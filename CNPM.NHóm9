#include <iostream>
#include <vector>
#include <string>
using namespace std;

// =======================
// STRUCT (DATABASE)
// =======================
struct User {
    string username;
    string password;
    string role; // guest, member, admin
};

struct Recipe {
    int id;
    string title;
    string content;
    bool approved;
};

vector<User> users;
vector<Recipe> recipes;
int recipeId = 1;

// =======================
// GUEST USE-CASES
// =======================
void registerAccount() {
    User u;
    cout << "Username: ";
    cin >> u.username;
    cout << "Password: ";
    cin >> u.password;
    u.role = "member";
    users.push_back(u);
    cout << "Register success!\n";
}

int login(string& role) {
    string user, pass;
    cout << "Username: ";
    cin >> user;
    cout << "Password: ";
    cin >> pass;

    for (int i = 0; i < users.size(); i++) {
        if (users[i].username == user && users[i].password == pass) {
            role = users[i].role;
            cout << "Login success!\n";
            return i;
        }
    }
    cout << "Login failed!\n";
    return -1;
}

void browseRecipe() {
    cout << "=== Approved Recipes ===\n";
    for (auto r : recipes) {
        if (r.approved)
            cout << r.id << ". " << r.title << endl;
    }
}

void viewRecipeDetail() {
    int id;
    cout << "Recipe ID: ";
    cin >> id;
    for (auto r : recipes) {
        if (r.id == id && r.approved) {
            cout << r.title << "\n" << r.content << endl;
            return;
        }
    }
    cout << "Recipe not found!\n";
}

// =======================
// MEMBER USE-CASES
// =======================
void postRecipe() {
    Recipe r;
    r.id = recipeId++;
    cout << "Title: ";
    cin.ignore();
    getline(cin, r.title);
    cout << "Content: ";
    getline(cin, r.content);
    r.approved = false;
    recipes.push_back(r);
    cout << "Recipe submitted (waiting approval)\n";
}

// =======================
// ADMIN USE-CASES
// =======================
void manageAllRecipes() {
    cout << "=== All Recipes ===\n";
    for (auto r : recipes) {
        cout << r.id << ". " << r.title
            << " | Approved: " << (r.approved ? "Yes" : "No") << endl;
    }
}

void approveRecipe() {
    int id;
    cout << "Recipe ID to approve: ";
    cin >> id;
    for (auto& r : recipes) {
        if (r.id == id) {
            r.approved = true;
            cout << "Recipe approved!\n";
            return;
        }
    }
    cout << "Recipe not found!\n";
}

// =======================
// MAIN MENU
// =======================
int main() {
    // Default admin
    users.push_back({ "admin", "admin", "admin" });

    int choice;
    string role;
    int currentUser = -1;

    do {
        cout << "\n=== WEBSITE CHIA SE CONG THUC NAU AN ===\n";
        cout << "1. Register\n";
        cout << "2. Login\n";
        cout << "3. Browse Recipe\n";
        cout << "4. View Recipe Detail\n";
        cout << "0. Exit\n";
        cout << "Choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            registerAccount();
            break;
        case 2:
            currentUser = login(role);
            if (currentUser != -1) {
                if (role == "member") {
                    postRecipe();
                }
                if (role == "admin") {
                    manageAllRecipes();
                    approveRecipe();
                }
            }
            break;
        case 3:
            browseRecipe();
            break;
        case 4:
            viewRecipeDetail();
            break;
        }
    } while (choice != 0);

    return 0;
}
