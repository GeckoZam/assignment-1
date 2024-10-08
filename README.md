# Actividad B2.1
**Alumno: Salazar Diaz Samuel**<br>
**No. Control: 19211729**
## Primer Giro de Ruleta
![imagen](https://github.com/user-attachments/assets/991c2da4-99b3-4512-a3e6-3d8952ef804a)

- **Categoría**: Creacional
- **Dominio**: Entretenimiento
- **Requisito**: Gestión de Estados y Ciclos de Vida
- **Patrón de Diseño Seleccionado**: Prototype

## Problema planteado
Imagina que estás creando un videojuego de rol (RPG) donde los jugadores pueden seleccionar personajes base, pero luego personalizarlos o mejorarlos. En lugar de crear cada personaje desde cero, el sistema puede clonar personajes prototipo (por ejemplo, un guerrero o un mago) y permitir que los jugadores los modifiquen o gestionen su estado durante el juego.

## Solución
Utilizaremos el patrón Prototype para clonar personajes de diferentes clases (guerrero, mago, arquero), y luego implementaremos funciones para gestionar su estado, como ciclos de vida (niveles de salud y energía) y habilidades.

### Codigo solución
```c#
using System;

// Step 1: Definir la interfaz Prototype (ICharacter) con gestión de estado
public interface ICharacter
{
    ICharacter Clone(); // Método para clonar el personaje
    void ShowStats();   // Método para mostrar el estado actual del personaje
    void TakeDamage(int amount);  // Método para gestionar daño
    void UseEnergy(int amount);   // Método para gestionar el uso de energía
    void Heal(int amount);        // Método para curar el personaje
    void RestoreEnergy(int amount);  // Método para restaurar energía
}

// Step 2: Implementar los prototipos concretos (Guerrero, Mago, Arquero)
public class Warrior : ICharacter
{
    public string Name { get; set; }
    public int Health { get; set; }
    public int Energy { get; set; }
    public string Weapon { get; set; }

    public Warrior(string name, string weapon)
    {
        Name = name;
        Health = 100;
        Energy = 50;
        Weapon = weapon;
    }

    // Clonar el Guerrero
    public ICharacter Clone()
    {
        return new Warrior(Name, Weapon)
        {
            Health = this.Health,
            Energy = this.Energy
        };
    }

    // Mostrar estadísticas del personaje
    public void ShowStats()
    {
        Console.WriteLine($"Guerrero {Name} - Salud: {Health}, Energía: {Energy}, Arma: {Weapon}");
    }

    // Métodos para gestionar el ciclo de vida
    public void TakeDamage(int amount)
    {
        Health -= amount;
        if (Health < 0) Health = 0;
        Console.WriteLine($"{Name} recibió {amount} puntos de daño. Salud restante: {Health}");
    }

    public void UseEnergy(int amount)
    {
        Energy -= amount;
        if (Energy < 0) Energy = 0;
        Console.WriteLine($"{Name} usó {amount} puntos de energía. Energía restante: {Energy}");
    }

    public void Heal(int amount)
    {
        Health += amount;
        if (Health > 100) Health = 100;
        Console.WriteLine($"{Name} se curó {amount} puntos de salud. Salud actual: {Health}");
    }

    public void RestoreEnergy(int amount)
    {
        Energy += amount;
        if (Energy > 50) Energy = 50;
        Console.WriteLine($"{Name} restauró {amount} puntos de energía. Energía actual: {Energy}");
    }
}

public class Mage : ICharacter
{
    public string Name { get; set; }
    public int Health { get; set; }
    public int Energy { get; set; }
    public string Spell { get; set; }

    public Mage(string name, string spell)
    {
        Name = name;
        Health = 80;
        Energy = 100;
        Spell = spell;
    }

    // Clonar el Mago
    public ICharacter Clone()
    {
        return new Mage(Name, Spell)
        {
            Health = this.Health,
            Energy = this.Energy
        };
    }

    public void ShowStats()
    {
        Console.WriteLine($"Mago {Name} - Salud: {Health}, Energía: {Energy}, Hechizo: {Spell}");
    }

    public void TakeDamage(int amount)
    {
        Health -= amount;
        if (Health < 0) Health = 0;
        Console.WriteLine($"{Name} recibió {amount} puntos de daño. Salud restante: {Health}");
    }

    public void UseEnergy(int amount)
    {
        Energy -= amount;
        if (Energy < 0) Energy = 0;
        Console.WriteLine($"{Name} usó {amount} puntos de energía. Energía restante: {Energy}");
    }

    public void Heal(int amount)
    {
        Health += amount;
        if (Health > 80) Health = 80;
        Console.WriteLine($"{Name} se curó {amount} puntos de salud. Salud actual: {Health}");
    }

    public void RestoreEnergy(int amount)
    {
        Energy += amount;
        if (Energy > 100) Energy = 100;
        Console.WriteLine($"{Name} restauró {amount} puntos de energía. Energía actual: {Energy}");
    }
}

// Step 3: Implementar el cliente (sistema de gestión de personajes)
class Program
{
    static void Main(string[] args)
    {
        // Crear personajes prototipo
        Warrior warriorPrototype = new Warrior("Aragorn", "Espada");
        Mage magePrototype = new Mage("Gandalf", "Rayo");

        // Clonar personajes a partir de los prototipos
        ICharacter warriorClone = warriorPrototype.Clone();
        ICharacter mageClone = magePrototype.Clone();

        // Mostrar estadísticas iniciales
        Console.WriteLine("Personajes originales:");
        warriorPrototype.ShowStats();
        magePrototype.ShowStats();

        Console.WriteLine("\nPersonajes clonados:");
        warriorClone.ShowStats();
        mageClone.ShowStats();

        // Simular ciclo de vida
        Console.WriteLine("\nSimulación de batalla:");
        warriorClone.TakeDamage(30);
        warriorClone.UseEnergy(20);
        warriorClone.Heal(15);
        warriorClone.RestoreEnergy(10);

        mageClone.TakeDamage(50);
        mageClone.UseEnergy(40);
        mageClone.Heal(25);
        mageClone.RestoreEnergy(50);
    }
}
```
## Explicación del código
1. Interfaz Prototype (ICharacter): Define el método Clone() para que los personajes puedan ser clonados. También define métodos para gestionar el estado del personaje, como tomar daño, usar energía, curarse y restaurar energía.
2. Clases concretas (Warrior, Mage): Estas clases representan diferentes tipos de personajes (guerrero y mago) que implementan la interfaz ICharacter. Ambos tienen atributos específicos como salud, energía y sus respectivas armas o hechizos. Además, cada uno tiene su propia lógica de gestión de estado.
3. Clonación: El método Clone() permite clonar personajes con el mismo estado que el original (como salud y energía). Esto permite crear rápidamente nuevos personajes sin tener que iniciar desde cero.
4. Gestión del Ciclo de Vida: Métodos como TakeDamage(), UseEnergy(), Heal() y RestoreEnergy() permiten gestionar el estado del personaje a lo largo de una batalla o evento. Estos métodos simulan el ciclo de vida del personaje, permitiendo cambios en sus atributos según lo que ocurra en el juego.

### Salida del codigo
```yaml
Personajes originales:
Guerrero Aragorn - Salud: 100, Energía: 50, Arma: Espada
Mago Gandalf - Salud: 80, Energía: 100, Hechizo: Rayo

Personajes clonados:
Guerrero Aragorn - Salud: 100, Energía: 50, Arma: Espada
Mago Gandalf - Salud: 80, Energía: 100, Hechizo: Rayo

Simulación de batalla:
Aragorn recibió 30 puntos de daño. Salud restante: 70
Aragorn usó 20 puntos de energía. Energía restante: 30
Aragorn se curó 15 puntos de salud. Salud actual: 85
Aragorn restauró 10 puntos de energía. Energía actual: 40
Gandalf recibió 50 puntos de daño. Salud restante: 30
Gandalf usó 40 puntos de energía. Energía restante: 60
Gandalf se curó 25 puntos de salud. Salud actual: 55
Gandalf restauró 50 puntos de energía. Energía actual: 100
```

## Segundo Giro de Ruleta
![imagen](https://github.com/user-attachments/assets/6c3a2853-adc6-4897-a9d5-c5b92f448eea)

- **Categoría**: Estructural
- **Dominio**: Industrial
- **Requisito**: Extensibilidad y Mantenibilidad
- **Patrón de Diseño Seleccionado**: Decorator
## Problema planteado
En una planta de fabricación, las máquinas de producción básicas necesitan ser mejoradas con características adicionales como control de temperatura, sensores de seguridad, y control de velocidad. El problema es que no queremos modificar el código original de la máquina para cada nueva característica, ya que eso haría el sistema difícil de mantener y extender.

## Solución
Usaremos el patrón Decorator para agregar funcionalidades adicionales a las máquinas de manera dinámica, sin modificar la clase base de la máquina. Cada decorador proporcionará una característica adicional (por ejemplo, control de temperatura o sensores de seguridad), permitiendo una arquitectura más flexible y extensible.

### Codigo solución
```c#
using System;

// Step 1: Definir la interfaz base (IMachine)
public interface IMachine
{
    void Operate();  // Método para realizar la operación de la máquina
}

// Step 2: Implementar la clase concreta (BasicMachine)
public class BasicMachine : IMachine
{
    public void Operate()
    {
        Console.WriteLine("Operando máquina básica.");
    }
}

// Step 3: Crear la clase base Decorator que implementa la interfaz de la máquina
public abstract class MachineDecorator : IMachine
{
    protected IMachine _machine;

    public MachineDecorator(IMachine machine)
    {
        _machine = machine;
    }

    public virtual void Operate()
    {
        _machine.Operate(); // Delegar la operación a la máquina básica
    }
}

// Step 4: Crear decoradores concretos para agregar funcionalidad adicional
public class TemperatureControlDecorator : MachineDecorator
{
    public TemperatureControlDecorator(IMachine machine) : base(machine) { }

    // Agregar la funcionalidad de control de temperatura
    public override void Operate()
    {
        base.Operate();
        Console.WriteLine("Controlando la temperatura de la máquina.");
    }
}

public class SpeedControlDecorator : MachineDecorator
{
    public SpeedControlDecorator(IMachine machine) : base(machine) { }

    // Agregar la funcionalidad de control de velocidad
    public override void Operate()
    {
        base.Operate();
        Console.WriteLine("Controlando la velocidad de la máquina.");
    }
}

public class SafetySensorDecorator : MachineDecorator
{
    public SafetySensorDecorator(IMachine machine) : base(machine) { }

    // Agregar la funcionalidad de sensores de seguridad
    public override void Operate()
    {
        base.Operate();
        Console.WriteLine("Monitoreando los sensores de seguridad.");
    }
}

// Step 5: Implementar el cliente para probar las máquinas con decoradores
class Program
{
    static void Main(string[] args)
    {
        // Crear una máquina básica
        IMachine basicMachine = new BasicMachine();
        Console.WriteLine("Máquina básica:");
        basicMachine.Operate();

        // Decorar la máquina con control de temperatura
        IMachine temperatureControlledMachine = new TemperatureControlDecorator(basicMachine);
        Console.WriteLine("\nMáquina con control de temperatura:");
        temperatureControlledMachine.Operate();

        // Decorar la máquina con control de temperatura y velocidad
        IMachine fullyControlledMachine = new SpeedControlDecorator(temperatureControlledMachine);
        Console.WriteLine("\nMáquina con control de temperatura y velocidad:");
        fullyControlledMachine.Operate();

        // Decorar la máquina con control de temperatura, velocidad y sensores de seguridad
        IMachine fullyEnhancedMachine = new SafetySensorDecorator(fullyControlledMachine);
        Console.WriteLine("\nMáquina con control de temperatura, velocidad y sensores de seguridad:");
        fullyEnhancedMachine.Operate();
    }
}
```
## Explicación del código
1. Interfaz base (IMachine): Define el método Operate() que representa el funcionamiento básico de la máquina.
2. Clase concreta (BasicMachine): Esta clase implementa la interfaz IMachine y representa una máquina simple que realiza una operación básica.
3. Clase base Decorator (MachineDecorator): Es una clase abstracta que implementa la interfaz IMachine. Esta clase contiene una referencia a una instancia de IMachine y delega la llamada a su método Operate(). Las subclases decoradoras extienden esta clase para añadir funcionalidad adicional sin modificar la máquina original.
4. Decoradores concretos:
    - TemperatureControlDecorator: Añade la funcionalidad de control de temperatura a la máquina.
    - SpeedControlDecorator: Añade la funcionalidad de control de velocidad a la máquina.
    - SafetySensorDecorator: Añade la funcionalidad de monitoreo de sensores de seguridad.
5. Cliente (Program): El cliente puede crear una máquina básica y agregarle decoradores según sea necesario. Cada decorador extiende el comportamiento de la máquina básica sin cambiar su código original.

### Salida del código
```yaml
Máquina básica:
Operando máquina básica.

Máquina con control de temperatura:
Operando máquina básica.
Controlando la temperatura de la máquina.

Máquina con control de temperatura y velocidad:
Operando máquina básica.
Controlando la temperatura de la máquina.
Controlando la velocidad de la máquina.

Máquina con control de temperatura, velocidad y sensores de seguridad:
Operando máquina básica.
Controlando la temperatura de la máquina.
Controlando la velocidad de la máquina.
Monitoreando los sensores de seguridad.
```
  
