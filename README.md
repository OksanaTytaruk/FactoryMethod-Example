# Factory Method Example

Цей репозиторій містить приклад патерну проектування "Фабричний метод".

## Фабричний метод (Factory Method)

Фабричний метод дозволяє створювати об'єкти, не вказуючи їх конкретні типи, а використовувати інтерфейси або абстрактні класи для цього. Він дозволяє відкладати створення об'єкта до моменту його використання та полегшує заміну конкретних класів.

### Приклад коду:

```csharp
// Product interface
public interface ITransport
{
    void Deliver();
}

// Concrete Products
public class Truck : ITransport
{
    public void Deliver()
    {
        Console.WriteLine("Delivery by truck");
    }
}

public class Ship : ITransport
{
    public void Deliver()
    {
        Console.WriteLine("Delivery by ship");
    }
}

// Creator class
public abstract class Logistics
{
    public abstract ITransport CreateTransport();

    public void PlanDelivery()
    {
        var transport = CreateTransport();
        transport.Deliver();
    }
}

// Concrete Creators
public class RoadLogistics : Logistics
{
    public override ITransport CreateTransport()
    {
        return new Truck();
    }
}

public class SeaLogistics : Logistics
{
    public override ITransport CreateTransport()
    {
        return new Ship();
    }
}

// Usage
class Program
{
    static void Main(string[] args)
    {
        Logistics logistics = new RoadLogistics();
        logistics.PlanDelivery();

        logistics = new SeaLogistics();
        logistics.PlanDelivery();
    }
}
