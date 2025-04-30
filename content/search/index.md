#include <iostream>
#include <vector>
#include <iomanip>
using namespace std;

struct MenuItem {
    int itemNumber;
    string itemName;
    float price;
};

vector<MenuItem> menuList;

void getData() {
    menuList.push_back({111, "Plain Egg", 1.45});
    menuList.push_back({112, "Bacon and Egg", 2.45});
    menuList.push_back({113, "Muffin", 0.99});
    menuList.push_back({114, "French Toast", 1.99});
    menuList.push_back({115, "Fruit Basket", 2.49});
    menuList.push_back({116, "Cereal", 0.69});
    menuList.push_back({117, "Coffee", 0.50});
    menuList.push_back({118, "Tea", 0.75});
}

void showMenu() {
    cout << "********Welcome to Meal Hut*********\n";
    cout << "Breakfast Billing System\n";
    cout << "Item No  Menu Item               Price\n";
    for (const auto& item : menuList) {
        cout << item.itemNumber << "      " << item.itemName << "    $" << fixed << setprecision(2) << item.price << endl;
    }
    cout << "Enter item numbers to select, -1 to finish.\n";
}

void printCheck(const vector<int>& selectedItems) {
    float total = 0.0;
    cout << "******** Bill ********\n";
    for (int itemNumber : selectedItems) {
        for (const auto& item : menuList) {
            if (item.itemNumber == itemNumber) {
                total += item.price;
                cout << item.itemName << "     $" << fixed << setprecision(2) << item.price << endl;
            }
        }
    }
    float tax = total * 0.05;
    float amountDue = total + tax;
    cout << "Tax                 $ " << fixed << setprecision(2) << tax << endl;
    cout << "Amount Due          $ " << fixed << setprecision(2) << amountDue << endl;
}

int main() {
    getData();
    showMenu();
    
    vector<int> selectedItems;
    int choice;
    while (true) {
        cout << "Enter item number (-1 to finish): ";
        cin >> choice;
        if (choice == -1) break;
        selectedItems.push_back(choice);
    }

    printCheck(selectedItems);
    return 0;
}


