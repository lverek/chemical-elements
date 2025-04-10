# chemical-elements
import json

class ChemicalElements:
    def __init__(self, file_name="elements.json"):
        self.file_name = file_name
        self.load_data()

    def load_data(self):
        """Load chemical elements data from a file or create a new one."""
        try:
            with open(self.file_name, "r", encoding="utf-8") as file:
                self.elements = json.load(file)
        except (FileNotFoundError, json.JSONDecodeError):
            self.elements = {}

    def save_data(self):
        """Save elements data to a file."""
        with open(self.file_name, "w", encoding="utf-8") as file:
            json.dump(self.elements, file, indent=4, ensure_ascii=False)

    def add_element(self, symbol, name, atomic_number, atomic_mass):
        """Add a new chemical element to the dictionary."""
        self.elements[symbol] = {
            "name": name,
            "atomic_number": atomic_number,
            "atomic_mass": atomic_mass
        }
        self.save_data()
        print(f"Added element: {symbol} ({name})")

    def get_element(self, symbol):
        """Retrieve element information by its symbol."""
        return self.elements.get(symbol, "Element not found.")

    def list_elements(self):
        """List all stored chemical elements."""
        if not self.elements:
            print("No elements recorded yet.")
            return
        for symbol, data in self.elements.items():
            print(f"{symbol}: {data['name']} (Atomic No: {data['atomic_number']}, Mass: {data['atomic_mass']})")

# Example usage
def main():
    elements_db = ChemicalElements()
    while True:
        print("\n🔬 Chemical Elements Database")
        print("1. Add an Element")
        print("2. Get Element Info")
        print("3. List All Elements")
        print("4. Exit")
        choice = input("Select an option: ")
        
        if choice == "1":
            symbol = input("Enter element symbol: ").strip()
            name = input("Enter element name: ").strip()
            atomic_number = int(input("Enter atomic number: "))
            atomic_mass = float(input("Enter atomic mass: "))
            elements_db.add_element(symbol, name, atomic_number, atomic_mass)
        elif choice == "2":
            symbol = input("Enter element symbol: ").strip()
            print(elements_db.get_element(symbol))
        elif choice == "3":
            elements_db.list_elements()
        elif choice == "4":
            break
        else:
            print("Invalid choice. Try again.")

if __name__ == "__main__":
    main()
34567
