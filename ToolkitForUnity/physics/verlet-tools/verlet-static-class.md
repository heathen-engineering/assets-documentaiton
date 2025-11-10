# Verlet (Static Class)

Utility class providing core Verlet integration functionality for particle motion and physics simulations. Supports time-corrected integration and spring-like acceleration via Hooke's Law.

The `Verlet` class contains:

* A stable time-corrected Verlet integration method, designed for variable deltaTime.
* A helper for computing restoring acceleration based on spring-like elasticity.

```csharp
csharpCopyEditpublic static class Verlet
{
    public static float3 TimeCorrectedVerletIntegration(...);
    public static float3 ElasticityAcceleration(...);
}
```

***

## Methods

### Time Corrected Verlet Integration

```csharp
csharpCopyEditpublic static float3 TimeCorrectedVerletIntegration(
    float3 currentPosition,
    float3 priorPosition,
    float3 acceleration,
    float currentTimestep,
    float priorTimestep)
```

**Description**

Performs **time-corrected Verlet integration**, which maintains stability when deltaTime changes frame-to-frame. This avoids the instability common in basic Verlet integration under variable framerate conditions.

**Parameters**

* **`currentPosition`** (`float3`)\
  Current position of the particle.
* **`priorPosition`** (`float3`)\
  Position of the particle in the previous frame.
* **`acceleration`** (`float3`)\
  Current acceleration (e.g., gravity or other forces).
* **`currentTimestep`** (`float`)\
  Delta time (`Time.deltaTime`) for the current frame.
* **`priorTimestep`** (`float`)\
  Delta time from the previous frame.

**Returns**

* **`float3`** — New particle position.

**Notes**

This method assumes consistent scaling of forces over time, and works well with dynamic frame rates.

***

### Elasticity Acceleration

```csharp
csharpCopyEditpublic static float3 ElasticityAcceleration(
    float mass,
    float3 displacement,
    float elasticity)
```

**Description**

Computes acceleration due to a **spring force** using Hooke's Law:

> F = -k \* x → a = F / m

Used to simulate spring-like connections, restoring forces, or soft constraints.

**Parameters**

* **`mass`** (`float`)\
  Mass of the object. Must be greater than 0.
* **`displacement`** (`float3`)\
  Offset from equilibrium (zero force) position.
* **`elasticity`** (`float`)\
  Spring constant (stiffness).

**Returns**

* **`float3`** — Acceleration vector pointing back toward the equilibrium.

**Notes**

Returns `float3.zero` if `mass <= 0` to avoid division errors.
