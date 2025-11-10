# Data Lens Table View

{% hint style="success" %}
**Note: These tools are in preview**\
We follow a “dogfood” development approach—these tools are actively used and developed within our current WIP games. They are mature enough to share with our GitHub and Patreon supporters, so their documentation is provided here for early adopters.
{% endhint %}

The `DataLensTableView` provides designers with a powerful, T-SQL-inspired query system to build dynamic views on game data. The key component driving this is the **DataLens Query** (`FDataLensQuery`), which defines what data to select, filter, aggregate, and how to relate records.

This article fully documents how to write queries, especially focusing on the **value expressions** used in `Select`, `Where`, and aggregation clauses.

## Creating a View

You will create your view derived from the `UDataLensTableView` class, you can do this in Blueprint of in C++.

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

You will need to provide Class defaults for&#x20;

* Target Struct Type\
  This is a USTRUCT that will be used to created the resulting TArray\<YourStruct> and is what we reflect against to sort out your field data types.
* Query\
  This provides the configuration for what records to read from where and how to filter them and how to map them to your target struct type. We dive into the Query Structure below.

## View Registration

To Be Done

Views are "churned" by the Subsystem so you will need to "Register" the view with the subsystem for it to be processed at run time. More on this later.

## Reading the View

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

The Get View Results tales the "View" type you wish to receive records for and returns the typed array of those records, You can then process them as you see fit. This "view" of those records is kept up-to-date by the system.

## Query Structure (`FDataLensQuery`)

```cpp
USTRUCT(BlueprintType)
struct FDataLensQuery
{
    GENERATED_BODY()
public:
    TArray<FDataLensFieldAddress> InputAliases;
    TArray<FDataLensFieldAddress> RelatedAliases;
    TArray<FLensTableViewColumn> Select;
    FGameplayTag From;
    TArray<FGameplayTag> Join;
    FString WhereClause;
    TArray<FName> GroupBy;
    TArray<FSortColumnByName> SortBy;
    FString HavingClause;
};
```

* **InputAliases**: Single related record attributes for quick reference by index `[n]`.
* **RelatedAliases**: Multi-related records for aggregate operations referenced as `{n}`.
* **Select**: Columns expressed as formulas using Input/Related aliases.
* **From**: The main source table.
* **Join**: Related tables joined.
* **WhereClause:** Filtering expression
* **HavingClause**: For future use, Grouping is only partly implemented later we "may" add full TSQL View like grouping, in which case this is part of that.
* **GroupBy:** Grouping controls, grouping is only partially implemented at the moment and may be removed. We are "inspired" by TSQL's Create View, but we are not a relational DB, we are actually more similar to a Graph DB so we may strip it or change it entirely.
* **SortBy**: Sorting controls.

### Understanding Field Addresses (`FDataLensFieldAddress`)

```cpp
USTRUCT(BlueprintType)
struct FDataLensFieldAddress
{
    GENERATED_BODY()

    FGameplayTag Source;    // Table or related record tag
    FGameplayTag Attribute; // Attribute on that table or related record
};
```

* **Source**: Either the main source table (`Query.From`) or a related record reference (a tag pointing to a related entity).
* **Attribute**: The attribute/property to read from the `Source`.

#### Example

* `Source = "NPCTable.Rel.Faction"` — the related Faction record linked to the NPC.
* `Attribute = "FactionTable.Attr.Level"` — the Level attribute of that Faction.

### Understanding View Column ( `FLensTableViewColumn` )

```cpp
USTRUCT(BlueprintType)
struct FLensTableViewColumn
{
    GENERATED_BODY()
public:
    FString Formula;
    FName ColumnName;
};
```

* **Formula**: the "expression" of how data should be mapped to this column
* **ColumnName**: the name of the property in the struct provided to the view where the result should be written.

***

### Aliases in Queries: `[n]` and `{n}`

#### Input Aliases `[n]`

* Represent **single related record attributes**.
* Indexed by their position in `InputAliases`.
* When used in expressions, `[0]` refers to the first Input Alias.
* Example:\
  If `InputAliases[0] = { Source: NPCTable.Rel.Faction, Attribute: FactionTable.Attr.Level }`\
  Then `[0]` in expressions reads the **Level of the NPC's Faction**.

#### Related Aliases `{n}`

* Represent **collections of related records** (e.g., multiple family members).
* Indexed by their position in `RelatedAliases`.
* Used primarily in aggregate functions.
* Example:\
  If `RelatedAliases[0] = { Source: NPCTable.Rel.FamilyMembers, Attribute: NPCTable.Attr.Rank }`\
  Then
  * `Sum({0})` sums the Rank attribute of all family members.
  * `CountIf({0}, > 2)` counts how many family members have Rank > 2.

***

### Expression Examples

#### Simple Arithmetic and Aggregation

* `[0] / 10` — reads attribute at InputAlias 0 and divides by 10 (e.g., health scaled to 2 decimals).
* `Sum({0}) + 1` — sums values of RelatedAlias 0 and adds 1.
* `SumIf({0}, > 3)` — sums values > 3 only.

#### Boolean Conditions (Where / Having Clauses)

* `[0] / 1000 >= 0.5` — true if attribute at InputAlias 0 is at least 50% of max (e.g., health check).
* `HasAny("Merchant", "ShopKeeper")` — true if the record has any of these traits.

#### Trait Counting

* `TraitCount("Merchant") + TraitCount("ShopKeeper") > 1`\
  True if the record has at least two of those traits.

***

### Summary

* **InputAliases** (`[n]`) point to a single related record's attribute for direct access.
* **RelatedAliases** (`{n}`) point to multiple related records' attributes for aggregation.
* Expressions combine these aliases with operators, aggregation functions (`Sum`, `CountIf`), and logical conditions to create flexible, designer-friendly data queries.

## Aggregate Operations

Aggregates only work on Related Record aliases, these are the  Field Addresses you populated in the Related Aliases collection of the Query. {0} for example means to use the first index of the RelatedAliases Field Addresses.

### Sum

Add up the values of the related expression.

#### Example:

```
Sum({0})
```

### SumIf

Add up the values if they pass the condition

#### Example:

```
SumIf({0}, >= 42)
```

### Avg

Find the average of values, e.g. Sum them all then divide by the number found. e.g. 5 entries with a total of 100 would be 20

```
Avg({0})
```

### Median

Find the mean of the values, e.g. find the min and max, take the difference between the max-min and divide by 2 adding that to the min. thu,s min = 10 max = 30 would return ((30-10)/2)+10 = 20

```
Median({0})
```

### Min

Find the smallest value in the related

```
Min({0})
```

### Max

Find the largest value in the related

```
Max({0})
```

### Count

Count the number of records in the target related

```
Count({0})
```

### CountIf

Count the number of records in the target related if the condition is met

```
CountIf({0}, >42)
```

### First

Get the value of the first record found in the related

```
First({0})
```

### Last

Get the value of the last record found in the related

```
Last({0})
```

## Trait Functions

Trait functions operate on tags and check the tag against the record being tested. note the inputs must be the "Name" of a tag this system uses Unreal's built-in GameplayTag system.

The Name must be quoted, you can use either " or ' to quote e.g. `"TagName"` or `'Tagname'` will work assuming TagName is the fully qualified name of a tag.\
\
You can use , or whitespace to delineate tags in the HasAll and HasAny e.g. `"TagName",'OtherTagName'` and `"TagName" 'OtherTagName'` will work

### HasTrait

This returns true if the trait is present on the record

```
HasTrait("TagName")
```

### TraitCount

This returns 0 if the trait is not present and 1 if it is. This is usually used to test if a record has "some" of a set of traits for example `TraitCount(Sword) + TraitCount(Axe) + TraitCount(Spear) > 2` would be true if the record as 2 or more of Sword, Axe and Spear.

#### Example

```
TraitCount("TagName")
```

### HasAny

This returns true if any of the traits listed ar present.

```
HasAny("TagName","OtherTagName","AnotherTagName")
```

### HasAll

This returns true if all the traits are present

```
HasAll("TagName","OtherTagName","AnotherTagName")
```

## Operators

These are operations that expect a value on the left and right side and perform basic math or logic operations. These work with Input Aliases such as `[0]`, Aggregate results `Sum({0})`, and Trait functions `TraitCount("TagName")`, as well as constants of course `42`.

### Parens

This lets you effect operation execution for example

```
([0] + 42) / ({1} - 15)
```

This would solve the operations within the parins first then solve the resulting equation.

### Add

Find the sum of the equation

#### Example:

```
[0] + 42
```

### Sub

Find the difference of the equation

#### Example:

```
[1] - 24
```

### Multiply

Find the product of the equation

```
[2] * {0}
```

### Division

Find the quotient of the equation

```
[3] / 2
```

### Greater Than

Return true if the left is greater than the right. This will return 1.0 or 0.0 for true and false when assigned to a numeric target or true and false when used in the where clause

```
[4] > 42
```

### Less Than

Return true if the left is less than the right. This will return 1.0 or 0.0 for true and false when assigned to a numeric target or true and false when used in the where clause

```
42 < [5]
```

### Greater Than or Equal To

Return true if the left is greater than or equal to the right. This will return 1.0 or 0.0 for true and false when assigned to a numeric target or true and false when used in the where clause

```
[2] >= 1
```

### Less Than or Equal To

Return true if the left is less than or equal to the right. This will return 1.0 or 0.0 for true and false when assigned to a numeric target or true and false when used in the where clause

```
[3] <= 42
```

### Equal To

Return true if the left is equal to the right. This will return 1.0 or 0.0 for true and false when assigned to a numeric target or true and false when used in the where clause

```
5 == Sum({2})
```

### Not Equal To

Return true if the left is not equal to the right. This will return 1.0 or 0.0 for true and false when assigned to a numeric target or true and false when used in the where clause

```
14 != CountIf({0}, >5)
```

### Logical And

Return true if the left and right are > 0. This will return 1.0 or 0.0 for true and false when assigned to a numeric target or true and false when used in the where clause

```
(4 > [1]) && HasAny("Tag1" "Tag2" "Tag3")
```

### Logical Or

Return true if the left or right are > 0. This will return 1.0 or 0.0 for true and false when assigned to a numeric target or true and false when used in the where clause

```
(4 > [1]) || HasAny("Tag1" "Tag2" "Tag3")
```

### Negative

Returns the negative of the right side e.g. "inverse"

```
-[0]
```

***

## Select Expressions

Select expressions define the data or values returned by a query. Effectively, these are your "Column Mappings" mapping some evaluation's output to a target field in the provided USTRUCT.

The "Select" is an array of[ `FLensTableViewColumn`,](data-lens-table-view.md#understanding-view-column-flenstableviewcolumn) which defines a formula and a column name.

```
Formula = CountIf({0}, > 17)
ColumnName = AdultFamilyMembers
```

The above assumes the first Related Alias is reading the Age attribute a Family Members related records. Thus, it's returning the number of Family Members whose age is > 17.

The data type of the target column determines the output type of the formula and can be Boolean, Float or Int32. Behind the curtain, we store everything as an int, process everything as a float and perform the final write via static\_cast. in the case of Boolean our internal rule is simply > 0 = true else false.

> If you try to map to a USTRUCT field that is not Boolean, Float or Int it will simply be ignored as an invalid mapping. In the editor, we do warn you of this but we never break, thus we are modder-friendly.



***

## Where Expressions

Where expressions define the "filter" for records, the where clause is "inclusive" meaning a record will process the where expression and if the result is "true" the record is added to the available records to map; if its false the record is skipped.

```
HasAny("Warrior", "Rogue", "Archer") && HasTrait("NPC")
```

You might use something like this to return a view of all the Character NPCs that are non-magic using class types.

Where Expressions do work with all operations, aggregates and trait functions. This is done via our "boolean" rule e.g. > 0 is true else false. That said you of course want to keep your where clause simple and fast making Traits the ideal aspect of a record to filter on.
