# codsoft_5
# Contact Manager Program

class Contact:
    def __init__(self, name, phone, email, address):
        self.name = name
        self.phone = phone
        self.email = email
        self.address = address

    def update_contact(self, name=None, phone=None, email=None, address=None):
        if name:
            self.name = name
        if phone:
            self.phone = phone
        if email:
            self.email = email
        if address:
            self.address = address

    def display_contact(self):
        print(f"Name: {self.name}")
        print(f"Phone: {self.phone}")
        print(f"Email: {self.email}")
        print(f"Address: {self.address}\n")


class ContactManager:
    def __init__(self):
        self.contacts = {}

    def add_contact(self):
        name = input("Enter name: ")
        phone = input("Enter phone number: ")
        email = input("Enter email: ")
        address = input("Enter address: ")
        self.contacts[phone] = Contact(name, phone, email, address)
        print("\nContact added successfully.\n")

    def view_contacts(self):
        if not self.contacts:
            print("\nNo contacts found.\n")
            return
        print("\nContact List:")
        for contact in self.contacts.values():
            print("----------------------")
            contact.display_contact()

    def search_contact(self):
        search_term = input("Enter name or phone number to search: ")
        found = False
        for contact in self.contacts.values():
            if search_term in contact.name or search_term == contact.phone:
                print("\nContact found:")
                print("----------------------")
                contact.display_contact()
                found = True
        if not found:
            print("\nContact not found.\n")

    def update_contact(self):
        phone = input("Enter phone number of contact to update: ")
        if phone in self.contacts:
            print("\nUpdating Contact:")
            name = input("Enter new name (leave blank to keep current): ")
            email = input("Enter new email (leave blank to keep current): ")
            address = input("Enter new address (leave blank to keep current): ")
            self.contacts[phone].update_contact(
                name=name or self.contacts[phone].name,
                email=email or self.contacts[phone].email,
                address=address or self.contacts[phone].address,
            )
            print("\nContact updated successfully.\n")
        else:
            print("\nContact not found.\n")

    def delete_contact(self):
        phone = input("Enter phone number of contact to delete: ")
        if phone in self.contacts:
            del self.contacts[phone]
            print("\nContact deleted successfully.\n")
        else:
            print("\nContact not found.\n")

    def display_menu(self):
        print("Contact Manager")
        print("1. Add Contact")
        print("2. View Contact List")
        print("3. Search Contact")
        print("4. Update Contact")
        print("5. Delete Contact")
        print("6. Exit")

    def run(self):
        while True:
            self.display_menu()
            choice = input("Choose an option: ")
            if choice == '1':
                self.add_contact()
            elif choice == '2':
                self.view_contacts()
            elif choice == '3':
                self.search_contact()
            elif choice == '4':
                self.update_contact()
            elif choice == '5':
                self.delete_contact()
            elif choice == '6':
                print("Exiting Contact Manager.")
                break
            else:
                print("Invalid option. Please try again.")


# Main program
if __name__ == "__main__":
    manager = ContactManager()
    manager.run()
