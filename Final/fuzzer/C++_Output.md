#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

// Define a lambda term
struct LambdaTerm {
    string var;
    vector<LambdaTerm*> args;
};

// Function to simplify a lambda term
LambdaTerm* simplify(LambdaTerm* term) {
    // Check if the term is a variable
    if (term->var != "") {
        return term;
    }

    // Check if the term is a lambda abstraction
    if (term->args.size() == 1) {
        LambdaTerm* arg = simplify(term->args[0]);
        if (arg->var != "") {
            return arg;
        }
    }

    // Check if the term is a function application
    if (term->args.size() > 1) {
        for (int i = 0; i < term->args.size(); i++) {
            term->args[i] = simplify(term->args[i]);
        }
        return term;
    }

    // If none of the above, return the original term
    return term;
}

int main() {
    // Define the lambda term
    LambdaTerm* term = new LambdaTerm();
    term->var = "";
    term->args.push_back(new LambdaTerm());
    term->args[0]->var = "";
    term->args[0]->args.push_back(new LambdaTerm());
    term->args[0]->args[0]->var = "";
    term->args[0]->args[0]->args.push_back(new LambdaTerm());
    term->args[0]->args[0]->args[0]->var = "";
    term->args[0]->args[0]->args[0]->args.push_back(new LambdaTerm());
    term->args[0]->args[0]->args[0]->args[0]->var = "";
    term->args[0]->args[0]->args[0]->args[0]->args.push_back(new LambdaTerm());
    term->args[0]->args[0]->args[0]->args[0]->args[0]->var = "";
    term->args[0]->args[0]->args[0]->args[0]->args[0]->args.push_back(new LambdaTerm());
    term->args[0]->args[0]->args[0]->args[0]->args[0]->args[0]->var = "";
    term->args[0]->args[0]->args[0]->args[0]->args[0]->args[0]->args.push_back(new LambdaTerm());
    term->args[0]->args[0]->args[0]->args[0]->args[0]->args[0]->args[0]->var = "";

    // Simplify the lambda term
    term = simplify(term);

    // Print the simplified lambda term
    cout << "Simplified lambda term: ";
    if (term->var != "") {
        cout << term->var;
    } else {
        cout << "(";
        for (int i = 0; i < term->args.size(); i++) {
            cout << simplify(term->args[i]);
            if (i < term->args.size() - 1) {
                cout << ", ";
            }
        }
        cout << ")";
    }
    cout << endl;

    return 0;
}
