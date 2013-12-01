ThoughtWorks Junior Consultant Coding Challenge
# PROBLEM TWO: SALES TAX

This application solves the sales tax problem by simulating an actual shopping experience. Data is input as a text file. Upon purchasing items, a receipt is printed that lists the name of all the items and their price (including tax), total cost, and total sales tax.

Basic sales tax is applicable at a rate of 10% on all goods, except books, food, and medical products that are exempt. Import duty is an additional sales tax applicable on all imported goods at a rate of 5%, with no exemptions.
 


# To run the app:
From the command line, run: checkout input/<filename>.txt

In the input folder, are three input text files with the data from this problem.

Pass in one of the provided input files in this format to get corresponding output in the form of a receipt:
  checkout input/input1.txt
    <!-- Results in Output 1 -->
  checkout input/input2.txt
    <!-- Results in Output 2 -->
  checkout input/input3.txt
    <!-- Results in Output 3 -->

Testing:

Testing was done using RSpec. Each class has a corresponding test file in the spec folder. 

Run bundle install to install the RSpec testing gem.

To run an individual test:
  rspec spec/<filename>.rb

To run all tests:
  rspec

#Design: 

The app has seven classes: Calculator, CommandLine, Government, InventoryFile, Item, Receipt, ShoppingCart. Each class is an abstraction of the real-world object it derives its name from. 

1. The Item class is responsible for creating new items and storing the name, price, taxable, and imported attributes. This class determines the tax type status of each item. If an item is taxable it is taxed at a rate of 10%; tax-exempt items are food, books, and medical supplies. If an item is imported, its is taxed at 5% (this applies to both taxable and tax-exempt items). 

2. The Government class sets the rules for what items are taxable and imported. In this app, only items that contain the following words in their names are tax-exempt: "book, chocolate, chocolates, headache pills." If the item's name contains the word "imported", it's imported tax status is set to true.  

3. The ShoppingCart class creates a cart in which to store items. Items can be added to and removed from the shopping cart, the quantity of a specific item in the cart can be changed, and the cart's contents can be viewed. When a user is finished shopping, the shopping cart is purchased, and a receipt is printed.

4. The Calculator class is responsible for the for tax calculations for each item based on it's tax type. The rounded sales tax and total taxed item price are calculated. 

5. The Receipt class is responsible for calculating the shopping cart sales tax and grand total. It is through this class that a receipt is printed out.

- Two classes are responsible for reading input data from text files so that the app can execute:

6. The InventoryFile class reads text files, parses input data so that items can be created, and adds these items to a shopping cart. The data is parsed so that each line of an input text file is a unique item. Each line is parsed using regular expression into three groupings. The first is the quantity, the second is the item name, and the third is the price ("at" is excluded). This data is used to create a new item and add it to the cart according to its quantity.

7. The CommandLine class is responsible for executing the app with a specified input text file and calling the purchase method on the resulting shopping cart. This runs the program and results in a receipt.

- Flow:
1. App is executed and a new CommandLine object is created, with an input text file passed to it.
2. The CommandLine object creates a new InventoryFile object.
3. The InventoryFile object reads the input file, creates items and shopping cart, and adds items to shopping cart. 
4. The CommandLine object purchases the shopping cart and a receipt is output.

#Assumptions:

1. Both item quantity and price are positive integers.
2. The input data is in the following format:
"(Quantity)(item) at (price)"
3. Since the items were limited for the scope of this exercise, only the keywords "book, chocolate, chocolates, headache pills" were used to determine if an item is tax-exempt. This does not include all types of food, books, or medical supplies. 
3. If an item's name included the word "imported", it was taxed as an imported item.
