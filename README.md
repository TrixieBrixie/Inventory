# Inventory

class Shoe:
    '''
    Constructor method with the following instance variables: 
    country, code, product, cost, quantity
    '''
    def __init__(self, country, code, product, cost, quantity):

        self.country = country
        self.code = code
        self.product = product
        self.cost = cost
        self.quantity = quantity
    
    def get_cost(self):
        # method to return the cost of the shoe
        return self.cost
    
    def get_quantity(self):
        # method to return the quantity of the shoes
        return self.quantity

    def __str__(self):
        # method to return a string representation of a class
        return f"{self.country}, {self.code}, {self.product}, {self.cost}, {self.quantity}"
        pass

def read_shoes_data():
    '''
    Function to read from the file inventory.txt, create a shoes object, 
    and append this object into the list_of_showes
    '''
    try:
        with open('inventory.txt', 'r') as file:

            next(file)
            for lines in file:
                temp = lines.strip().split(',')
                list_of_shoes.append(Shoe(temp[0], temp[1], temp[2], temp[3], temp[4]))
                for shoe in list_of_shoes:
                    print(shoe)

    except FileNotFoundError:
        print("Error: File not found.")
    
def capture_shoes():
    '''
    This function will allow a user to capture
    data about a shoe and use this data to create a shoe object
    and append this object inside the list_of_shoes
    '''
    country = input("What country are the shoes made from?: ")
    code = input("What's the shoe's unique code?: ")
    product = input("What's the name of the shoe?: ")
    cost = float(input("What's the price?: "))
    quantity = int(input("What's the quantity?: "))

    # Create a new Shoe object where to store user shoe info
    new_shoe = Shoe(country, code, product, cost, quantity)
    for shoes in list_of_shoes:
        # Making sure that a new shoe data does not have the same code of any shoe alreay in the list
        if new_shoe.code == shoes.code: 
            print("The code you have entered already exist:")
            print("Please provide a new code: ")
        else:
    # Add the new shoe to the list of shoes
            list_of_shoes.append(new_shoe)
    
    print("Shoe added successfully!")

def view_all():
    '''
    This function will iterate over all the shoes in the list and
    print the details of the shoes that returns from the __str__
    function.
    '''
    for shoes in list_of_shoes:
        print(shoes)

def re_stock(): 
    # Function that finds the shoe object with the lowest quantity
    quantities = [shoe.quantity for shoe in list_of_shoes]
    min_quantity = min([int(elements) for elements in quantities])
    low_stock_shoe = None
    for shoe in list_of_shoes:
        if int(shoe.quantity) == min_quantity:
            low_stock_shoe == shoe
            print(f"{shoe.product} is the product with the lowest quantity")
            break

    # Ask the user if he wants to add the quantity of these shoes and then update it
    add_quantity = input("would you like to add the quantity of these shoes? (Yes or No): ")
    if add_quantity == "Yes":
        num_of_pairs = int(input("How mamy pairs would you like to add?: "))
        updated_quantity = quantities + num_of_pairs
        min_quantity.append(updated_quantity)
    else:
        print("Retunr to menue.")

def search_shoe():
    # function that searches for a shoe from the list using the shoe code
    shoe_code = input("Please enter the shoe code: ")
    for shoe in list_of_shoes:
        if shoe.code == shoe_code: 
            print(shoe)

def value_per_item():
    # function that calculates the total value for each item
    for shoe in list_of_shoes:
        value = int(shoe.cost) * int(shoe.quantity)
        print(f"{shoe.product} - Total value: {value}")

def highest_qty():
    # Write code to determine the product with the highest quantity and print this shoe as being for sale.
    max_quantity = [shoe.quantity for shoe in list_of_shoes]
    quantities = max([(elements) for elements in max_quantity])
    low_stock_shoe = None
    for shoe in list_of_shoes:
        if (shoe.quantity) == quantities:
            low_stock_shoe == shoe
            print(f"{shoe.product} is the product with the highest quantity")
        
usage_message = '''
Welcome to the Nike warehouse store system! What would you like to do?

i - Read the invetory.
r - Record data about a shoe.
v - View all
rs - Restock
s - Search shoe
v - Value per item
h - highest_quantity
'''

list_of_shoes = []

while True:
    user_choice = input(usage_message).strip().lower()
    if user_choice == "i":
        # Call the funciton to print out the whole inventory
        read_shoes_data()
    elif user_choice == "r":
       # Call the function to store data about a new shoe
       capture_shoes()
    elif user_choice == "v":
        # Call the function to print out the whole list_of_shoes
        view_all()
    elif user_choice == 'rs':
        # Call the funciton to find the shoe object with the lowest quantity
        re_stock()
    elif user_choice == 's':
        # Call the funciton to search for a shoe from the list using the shoe code
        search_shoe()
    elif user_choice == 'v':
        # Call the funciton to calculate the total value for each item
        value_per_item()
    elif user_choice == "i":
        # Call the funciton to determine the product with the highest quantity
        highest_qty()
    else:
        print("Invalid choice. Please try again.")
        

