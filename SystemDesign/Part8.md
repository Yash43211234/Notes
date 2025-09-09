# 🔧 Low-Level Design (LLD) — Detailed Notes

---

## 1. OOP Design Principles (Easy language)

### SOLID (five short rules)
- **S — Single Responsibility Principle (SRP):**  
  A class should have one job. If it has more than one reason to change, split it.

- **O — Open/Closed Principle (OCP):**  
  Classes should be open for extension but closed for modification. Add new behavior by adding classes, not changing old ones.

- **L — Liskov Substitution Principle (LSP):**  
  Subclasses must be usable anywhere their base class is used. Don’t break expected behavior.

- **I — Interface Segregation Principle (ISP):**  
  Prefer many small interfaces over one large one. Clients should depend only on methods they use.

- **D — Dependency Inversion Principle (DIP):**  
  High-level modules should not depend on low-level modules directly. Both should depend on abstractions (interfaces).

---

## 2. Class Diagrams & Relationships (easy rules)

### Main relationship types
- **Association:** one class uses another (has-a).  
- **Aggregation:** a whole-part relationship but parts can exist independently.  
- **Composition:** a stronger whole-part where parts do not exist if whole is destroyed.  
- **Inheritance:** `is-a` relationship (base → derived).  
- **Dependency:** one class depends on another temporarily (method param).

### Tips to draw class diagrams simply
- Each class: `ClassName` with fields and main methods.
- Show arrows:
  - Solid line with open arrow → inheritance.
  - Plain line → association.
  - Diamond (empty) → aggregation; filled diamond → composition.
- Keep classes small (SRP). If a class has many responsibilities, split.

---

## 3. Useful Design Patterns (short + example use-case)

### Creational
- **Factory:** create objects without exposing creation logic.  
  Use when object creation is complex or varies by params.
- **Singleton:** one instance globally (e.g., configuration manager, connection pool).  
  Use carefully — singletons can hide dependencies.

### Structural
- **Adapter:** make one interface work with another (legacy -> new).  
- **Facade:** simple API in front of complex subsystems (e.g., PaymentFacade).

### Behavioral
- **Observer:** subscribers notified of events (e.g., UI events, pub/sub).  
- **Strategy:** swap algorithms at runtime (e.g., sorting, pricing strategy).  
- **Builder:** build complex objects step-by-step (useful for objects with many optional fields).

---

## 4. LLD Example 1 — Parking Lot (compact design)

### Requirements (simple)
- Multiple vehicle types (Car, Bike, Truck).  
- Different slot types (Compact, Large, Motorcycle).  
- Park, unpark, find nearest free slot, maintain fees.

### Key classes (UML-style list)
- `ParkingLot` (composition → contains Levels)
- `Level` (contains ParkingSpots)
- `ParkingSpot` (fields: id, type, isFree)
- `Vehicle` (base) → `Car`, `Bike`, `Truck`
- `Ticket` (ticketId, vehicle, spot, entryTime)
- `ParkingStrategy` (interface) — implementations: `NearestFirstStrategy`
- `ParkingFeeCalculator` (strategy for fee)

### Class sketch (pseudo-Java)
```java
class ParkingLot {
  String id;
  List<Level> levels;
  ParkingStrategy strategy;
  Ticket parkVehicle(Vehicle v) { ... }
  void unparkVehicle(Ticket t) { ... }
}

class Level {
  int levelNumber;
  List<ParkingSpot> spots;
  Optional<ParkingSpot> findSpot(Vehicle v) { ... }
}

class ParkingSpot {
  String id;
  SpotType type; // COMPACT, LARGE, MOTORCYCLE
  boolean isFree;
  void occupy(Vehicle v) { ... }
  void free() { ... }
}

abstract class Vehicle {
  String plateNumber;
  VehicleSize size; // SMALL, MEDIUM, LARGE
}
class Car extends Vehicle { }
class Bike extends Vehicle { }

class Ticket {
  String ticketId;
  String spotId;
  long entryTime;
  long exitTime;
}
```