#include <iostream>
#include <iomanip>
#include <vector>
using namespace std;

const double TAX_RATE = 0.05;
const int MENU_SIZE = 8;

struct MenuItem {
    int itemNo;
    string name;
    double price;
};

void getData(MenuItem menu[]) {
    menu[0] = {111, "Plain Egg", 1.45};
    menu[1] = {112, "Bacon and Egg", 2.45};
    menu[2] = {113, "Muffin", 0.99};
    menu[3] = {114, "French Toast", 1.99};
    menu[4] = {115, "Fruit Basket", 2.49};
    menu[5] = {116, "Cereal", 0.69};
    menu[6] = {117, "Coffee", 0.50};
    menu[7] = {118, "Tea", 0.75};
}

void showMenu(MenuItem menu[]) {
    cout << "********Welcome to Meal Hut*********\n";
    cout << "          Breakfast Billing System\n\n";
    cout << left << "Item No\tMenu Item\t\tPrice\n";
    for (int i = 0; i < MENU_SIZE; i++) {
        cout << menu[i].itemNo << "\t" << left << setw(20) << menu[i].name 
             << "$" << fixed << setprecision(2) << menu[i].price << endl;
    }
    cout << "\nEnter 0 to finish your order.\n";
}

void printCheck(vector<MenuItem> orderItems, vector<int> quantities) {
    double subtotal = 0.0;
    cout << "\n********Your Receipt********\n";
    cout << left << "Item\t\t\tPrice\n";

    for (size_t i = 0; i < orderItems.size(); i++) {
        double itemTotal = orderItems[i].price * quantities[i];
        subtotal += itemTotal;
        cout << left << setw(20) << orderItems[i].name 
             << "$" << fixed << setprecision(2) << itemTotal << endl;
    }

    double tax = subtotal * TAX_RATE;
    double total = subtotal + tax;

    cout << "Tax\t\t\t$" << fixed << setprecision(2) << tax << endl;
    cout << "Amount Due\t\t$" << total << endl;
}

int findMenuItem(MenuItem menu[], int code) {
    for (int i = 0; i < MENU_SIZE; i++) {
        if (menu[i].itemNo == code)
            return i;
    }
    return -1;
}

int main() {
    MenuItem menu[MENU_SIZE];
    vector<MenuItem> orderItems;
    vector<int> quantities;

    getData(menu);
    
    int choice, qty;
    do {
        showMenu(menu);
        cout << "Enter Item No: ";
        cin >> choice;
        
        if (choice == 0) break;

        int index = findMenuItem(menu, choice);
        if (index != -1) {
            cout << "Enter quantity: ";
            cin >> qty;
            if (qty > 0) {
                orderItems.push_back(menu[index]);
                quantities.push_back(qty);
            } else {
                cout << "Invalid quantity. Try again.\n";
            }
        } else {
            cout << "Invalid Item No. Try again.\n";
        }
    } while (true);

    if (!orderItems.empty()) {
        printCheck(orderItems, quantities);
    } else {
        cout << "No items ordered.\n";
    }

    return 0;

