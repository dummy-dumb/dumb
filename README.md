#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
};

Node* neew(int data) {
    Node* p = new Node(); // Allocate memory for Node in heap
    p->data = data;       // Set data
    p->left = nullptr;    // Set left and right node
    p->right = nullptr;
    return p;
}

void preOrder(Node* root) {
    if (root != nullptr) {
        cout << root->data << " ";
        preOrder(root->left);
        preOrder(root->right);
    }
}

void inOrder(Node* root) {
    if (root != nullptr) {
        inOrder(root->left);
        cout << root->data << " ";
        inOrder(root->right);
    }
}

void postOrder(Node* root) {
    if (root != nullptr) {
        postOrder(root->left);
        postOrder(root->right);
        cout << root->data << " ";
    }
}

int main() {    
    Node* n = neew(4);
    //     4
    //    / \
    //   1   6
    //  / \
    // 5   2
    n->left = neew(1);
    n->right = neew(6);
    n->left->left = neew(5);
    n->left->right = neew(1);

    cout << "PREORDER: ";
    preOrder(n);
    cout << endl;

    cout << "INORDER: ";
    inOrder(n);
    cout << endl;

    cout << "POSTORDER: ";
    postOrder(n);
    cout << endl;

    return 0;
}



#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
};

Node* createNode(int data) {
    Node* n = new Node();
    n->data = data;
    n->left = nullptr;
    n->right = nullptr;
    return n;
}

// Pre-order Traversal
void PreOrder(Node* root) {
    if (root != nullptr) {
        cout << root->data << " ";
        PreOrder(root->left);
        PreOrder(root->right);
    }
}

// Height
int Height(Node* root) {
    if (root != nullptr) {
        int leftHeight = Height(root->left);
        int rightHeight = Height(root->right);
        return max(leftHeight, rightHeight) + 1;     
    }
    return 0;
}

// Sum of nodes
int sum(Node* root) {
    if (root != nullptr) {
        int x = sum(root->left);
        int y = sum(root->right);
        return x + y + root->data;
    }
    return 0;
}

// Counting Nodes
int Count(Node* root) {
    if (root != nullptr) {
        int x = Count(root->left);
        int y = Count(root->right);
        return x + y + 1;
    }
    return 0;
}

// Count Leaf Nodes
int countLeafNodes(Node* root) {
    if (root == nullptr) {
        return 0;
    }
    if (root->left == nullptr && root->right == nullptr) {
        return 1; // Leaf node
    }
    return countLeafNodes(root->left) + countLeafNodes(root->right);
}

// Print Leaf Nodes
void printLeaf(Node* root) {
    if (root == nullptr) {
        return;
    }
    if (root->left == nullptr && root->right == nullptr) {
        cout << root->data << " ";
    }
    printLeaf(root->left);
    printLeaf(root->right);
}

// Create Mirror Image of Tree
Node* createMirror(Node* root) {
    if (root == nullptr) {
        return nullptr;
    }

    Node* mirror = createNode(root->data);
    mirror->left = createMirror(root->right);
    mirror->right = createMirror(root->left);

    return mirror;
}

int main() {
    Node* root = createNode(1);
    root->left = createNode(2);
    root->right = createNode(3);
    root->left->left = createNode(4);
    root->left->right = createNode(5);
    root->right->left = createNode(6);
    root->right->right = createNode(7);

    int choice;
    Node* mirrorRoot = nullptr;
    do {
        cout << "\n1. Height of the Tree\n";
        cout << "2. Sum of Nodes\n";
        cout << "3. Count Nodes\n";
        cout << "4. Count Leaf Nodes\n";
        cout << "5. Print Leaf Nodes\n";
        cout << "6. Create Mirror Image\n";
        cout << "7. Exit\n";

        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Height of the tree is: " << Height(root) << endl;
                break;

            case 2:
                cout << "Sum of nodes is: " << sum(root) << endl;
                break;

            case 3:
                cout << "Total number of nodes: " << Count(root) << endl;
                break;

            case 4:
                cout << "Number of Leaf Nodes: " << countLeafNodes(root) << endl;
                break;

            case 5:
                cout << "Leaf Nodes: ";
                printLeaf(root);
                cout << endl;
                break;

            case 6:
                cout << "Creating Mirror Image..." << endl;
                mirrorRoot = createMirror(root);
                cout << "Mirror Image created." << endl;
                cout << "Pre-order Traversal of Mirror Image: ";
                PreOrder(mirrorRoot);
                cout << endl;
                break;

            case 7:
                cout << "Exiting program." << endl;
                break;

            default:
                cout << "Invalid choice. Please enter a valid option." << endl;
        }
    } while (choice != 7);

    return 0;
}


