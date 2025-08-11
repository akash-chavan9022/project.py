''''
28/07/2025


Problem Statement: Library Management System (LMS)
Objective:
Create a menu-driven Library Management System using Python that allows library staff to log in, manage books, register members, issue and return books, and maintain all relevant data. The system should be simple but modular and scalable.

User Roles:
Admin (Librarian)

Username/Password-based login system

Only after login can operations be performed

Logout to end session

Modules and Functional Requirements:
1. Login System
Predefined credentials for the admin.

Validate username and password before giving access.

Retry option for wrong login attempts (max 3 tries).

2. Book Management
Add Book

Book ID (unique), Title, Author, Category, Quantity

View All Books

Display all books in tabular format

Update Book Info

Update book title, author, or quantity using Book ID

Delete Book

Remove a book by its Book ID

Search Book

By title or author name


3. Member Management
Register Member

Member ID (auto-generated), Name, Email, Mobile

View All Members

Display member details

Update Member Info

Edit name or contact info

Delete Member

Remove a member by Member ID

4. Issue and Return System
Issue Book

Input: Member ID and Book ID

Check book availability

Update quantity and maintain issue record with date

Return Book

Input: Member ID and Book ID

Update quantity

Remove from issue record

View Issued Books

List all issued books with member name and issue date

5. Logout System
End the admin session

Return to login screen

Data Structures:
Use Python dictionaries or lists of dictionaries to store:

Book Records

Member Records

Issue Records

Admin Credentials Example:

admin_credentials = {
    'admin': 'admin123'
}
Sample Data Structures:
Book Example:

books = {
    'B101': {'title': 'Python Basics', 'author': 'John Doe', 'category': 'Programming', 'quantity': 5}
}
Member Example:

members = {
    'M101': {'name': 'Alice', 'email': 'alice@example.com', 'mobile': '9876543210'}
}
Issue Record Example:
issued_books = [
    {'member_id': 'M101', 'book_id': 'B101', 'issue_date': '2025-07-28'}
]
'''

#Problem Statement: Library Management System (LMS)
# Objective:
# Create a menu-driven Library Management System using Python that allows library staff to log in, manage books, register members, issue and return books, and maintain all relevant data. The system should be simple but modular and scalable.


# Initial Data
# ------------------- Initial Data -------------------
# ------------------- Initial Data -------------------
books = {
    'B101': {'title': 'Python Basics', 'author': 'John Doe', 'category': 'Programming', 'quantity': 5}
}

members = {
    'M101': {'name': 'Alice', 'email': 'alice@example.com', 'mobile': '9876543210'}
}

issued_books = [{'member_id': 'M101', 'book_id': 'B101', 'issue_date': '2025-07-28'}]

admin_credentials = {
    'admin': 'admin123',
    'akash': 'akash123'
}

# ------------------- Login -------------------
username = input("UserName: ")
password = input("Password: ")

if username in admin_credentials and admin_credentials.get(username) == password:
    print("\n Login successful!")

    while True:
        print("\n===== Main Menu =====")
        print("1. Book Management")
        print("2. Member Management")
        print("3. Logout")
        ch = int(input("Enter your choice: "))

        # ------------------- Book Management -------------------
        if ch == 1:
            while True:
                print(f'\n1. Add Book\n2. Display Books\n3. Delete Book\n4. Filter by Category\n5. Search Book\n6. Back to Main Menu')
                ch1 = int(input("Enter your choice: "))

                # Add Book
                if ch1 == 1:
                    title = input("Enter the title of the book: ")
                    author = input("Enter the author of the book: ")
                    category = input("Enter the category of the book: ")
                    quantity = int(input("Enter the quantity of the book: "))
                    book_id = f'B{101 + len(books)}'
                    books[book_id] = {
                        'title': title,
                        'author': author,
                        'category': category,
                        'quantity': quantity
                    }
                    print("\n Book added successfully!")

                # Display Books
                elif ch1 == 2:
                    if books:
                        print('-' * 100)
                        print('|{:^10}|{:^25}|{:^20}|{:^20}|{:^10}|'.format('Book ID', 'Title', 'Author', 'Category', 'Qty'))
                        print('-' * 100)
                        for book_id, book in books.items():
                            print('|{:^10}|{:^25}|{:^20}|{:^20}|{:^10}|'.format(
                                book_id, book['title'], book['author'], book['category'], book['quantity']))
                        print('-' * 100)
                    else:
                        print("No books available.")

                # Delete Book
                elif ch1 == 3:
                    book_id = input("Enter the book ID to delete: ")
                    if book_id in books:
                        del books[book_id]
                        print(" Book deleted successfully.")
                    else:
                        print(" Book not found.")

                # Filter by Category
                elif ch1 == 4:
                    category = input("Enter the category to filter: ")
                    found = False
                    for book_id, book in books.items():
                        if book['category'].lower() == category.lower():
                            print(f"\nBook ID: {book_id}")
                            print(f"Title: {book['title']}")
                            print(f"Author: {book['author']}")
                            print(f"Quantity: {book['quantity']}")
                            found = True
                    if not found:
                        print("No books found in this category.")

                # Search Book
                elif ch1 == 5:
                    keyword = input("Enter title or author to search: ").lower()
                    found = False
                    for book_id, book in books.items():
                        if keyword in book['title'].lower() or keyword in book['author'].lower():
                            print(f"\nBook ID: {book_id}")
                            print(f"Title: {book['title']}")
                            print(f"Author: {book['author']}")
                            print(f"Category: {book['category']}")
                            print(f"Quantity: {book['quantity']}")
                            found = True
                    if not found:
                        print("No matching books found.")

                # Back to Main Menu
                elif ch1 == 6:
                    break
                else:
                    print(" Invalid choice. Try again.")

        # ------------------- Member Management -------------------
        elif ch == 2:
            while True:
                print(f'\n1. Register Member\n2. Display Members\n3. Update Member Info\n4. Delete Member\n5. Back to Main Menu')
                ch2 = int(input("Enter your choice: "))

                # Register Member
                if ch2 == 1:
                    name = input("Enter member name: ")
                    email = input("Enter email address: ")
                    mobile = input("Enter mobile number: ")
                    member_id = f'M{101 + len(members)}'
                    members[member_id] = {
                        'name': name,
                        'email': email,
                        'mobile': mobile
                    }
                    print(f"\n Member registered successfully with Member ID: {member_id}")

                # Display Members
                elif ch2 == 2:
                    if members:
                        print('-' * 90)
                        print('|{:^10}|{:^20}|{:^30}|{:^20}|'.format('Member ID', 'Name', 'Email', 'Mobile'))
                        print('-' * 90)
                        for member_id, m in members.items():
                            print('|{:^10}|{:^20}|{:^30}|{:^20}|'.format(member_id, m['name'], m['email'], m['mobile']))
                        print('-' * 90)
                    else:
                        print("No members registered.")

                # Update Member Info
                elif ch2 == 3:
                    member_id = input("Enter Member ID to update: ")
                    if member_id in members:
                        print("Leave blank to keep current value.")
                        name = input("Enter new name: ")
                        email = input("Enter new email: ")
                        mobile = input("Enter new mobile: ")
                        if name:
                            members[member_id]['name'] = name
                        if email:
                            members[member_id]['email'] = email
                        if mobile:
                            members[member_id]['mobile'] = mobile
                        print(" Member information updated.")
                    else:
                        print(" Member not found.")

                # Delete Member
                elif ch2 == 4:
                    member_id = input("Enter Member ID to delete: ")
                    if member_id in members:
                        del members[member_id]
                        print(" Member deleted successfully.")
                    else:
                        print(" Member not found.")

                # Back to Main Menu
