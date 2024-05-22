//TRAVERSAL
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


//TREE OPERATIONS
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


//BST INS SRCH DEL
#include <iostream>
using namespace std;

struct Node{
    int data;
    Node *left;
    Node *right;
};

void preOrder(Node*root){
    if(root!=NULL){
        cout<<root->data<<" ";
        preOrder(root->left);
        preOrder(root->right);
    }
}

Node* neew(int n){
    Node* node=new Node();
    node->data=n;
    node->left=nullptr;
    node->right=nullptr;
    return node;
}

Node*search(Node*root,int key){
    if (root == nullptr || root->data == key)
        return root;

    if (root->data < key)
        return search(root->right, key);
    
    return search(root->left, key);

}

Node* insert(Node*root,int key){
    if (root == nullptr) {
        return neew(key);
    }
   
    if (key < root->data) {
        root->left = insert(root->left, key);
    } 
    else {
        root->right= insert(root->right, key);
    } 
    return root;
}

Node* minValueNode(Node* node) {
    Node* current = node;

       while (current && current->left != nullptr)
        current = current->left;

    return current;
}

Node* deleteNode(Node* root, int key) {    
    if (root == nullptr) 
    return root;
    
    if (key < root->data)
        root->left = deleteNode(root->left, key);
    else if (key > root->data)
        root->right = deleteNode(root->right, key);

    else {        
        if (root->left == nullptr) {
            Node* temp = root->right;
            delete root;
            return temp;
        }if (root->right == nullptr) {
            Node* temp = root->left;
            delete root;
            return temp;
        }
        
        Node* temp = minValueNode(root->right);
        root->data = temp->data;

        root->right = deleteNode(root->right, temp->data);
    }
    return root;
}

void deleteBST(Node* root) {
    if (root == nullptr) return;
    deleteBST(root->left);
    deleteBST(root->right);
    delete root;
}

int main(){
    Node *root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    cout << "Inorder traversal of the BST: ";
    preOrder(root);
    cout << endl;

    int key = 20;
    Node* found = search(root, key);
    if (found)
        cout << key << " found in the BST\n";
    else
        cout << key << " not found in the BST\n";

    root = deleteNode(root, key);
    cout << "Inorder traversal after deletion of " << key << ": ";
    preOrder(root);
    cout << endl;

    deleteBST(root);
    return 0;

    return 0;
}



//TRAVERSAL ITERATIVE
#include <iostream>
#include <stack>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

void preorderTraversal(TreeNode* root) {
    if (root == NULL)return;        
    stack<TreeNode*> st;
    TreeNode* current = root;
    while (current != NULL || !st.empty()) {
        while (current != NULL) {
            cout << current->val << " ";
            st.push(current);       
            current = current->left;
        }
        current = st.top();     
        st.pop();       
        current = current->right;
    }
}

void inorderTraversal(TreeNode* root) {
    if (root == NULL)return;        
    stack<TreeNode*> st;
    TreeNode* current = root;
    while (current != NULL || !st.empty()) {
        while (current != NULL) {
            st.push(current);       
            current = current->left;
        }
        current = st.top();   
        cout << current->val << " ";
        st.pop();
        //cout << current->val << " ";
        current = current->right;
    }
}

void postorderTraversal(TreeNode* root) {
    if (root == NULL)
        return;

    stack<TreeNode*> st1, st2;
    TreeNode* current = root;
    st1.push(current);

    while (!st1.empty()) {
        current = st1.top();
        st1.pop();
        st2.push(current);

        if (current->left!=NULL)
            st1.push(current->left);

        if (current->right!=NULL)
            st1.push(current->right);
    }
    while (!st2.empty()) {
        current = st2.top();
        st2.pop();
        cout << current->val << " ";
    }
}

int main() {
    TreeNode* root = new TreeNode(10);
    root->left = new TreeNode(5);
    root->right = new TreeNode(11);
    root->left->left = new TreeNode(2);
    root->left->right = new TreeNode(8);
    root->right->right = new TreeNode(12);
    
    cout << "preorder traversal: ";
    preorderTraversal(root);
    cout << endl;
    
     cout << "inorder traversal: ";
    inorderTraversal(root);
    cout << endl;
    
     cout << "postorder traversal: ";
    postorderTraversal(root);
    cout << endl;

    return 0;
}




//AVL
#include <iostream>
using namespace std;

struct Node{
    Node *lchild;
    Node *rchild;
    int data;
    int height;
}
*root=nullptr;

int nodeHeight(Node *p){
    int hl,hr;
    hl=p&& p->lchild?p->lchild->height:0;
    hr=p&& p->rchild?p->rchild->height:0;
    return hl>hr?hl+1:hr+1;
}

int balanceFactor(Node *p){
    int hl,hr;
    hl=p&& p->lchild?p->lchild->height:0;
    hr=p&& p->rchild?p->rchild->height:0;
    return hl-hr;
}

Node*LLrot(Node *p){
    Node *pl=p->lchild;
    Node *plr=pl->rchild;
    pl->rchild=p;
    p->lchild=plr;
    p->height=nodeHeight(p);
    pl->height=nodeHeight(pl);

    if(root==p) root=pl;
    return pl;
}

Node*RRrot(Node *p){
    Node *pr=p->rchild;
    Node *prl=pr->lchild;
    pr->lchild=p;
    p->rchild=prl;
    p->height=nodeHeight(p);
    pr->height=nodeHeight(pr);
    
    if(root==p) root=pr;
    return pr;
}

Node*LRrot(Node *p){
    Node *pl=p->lchild;
    Node *plr=pl->rchild;
    pl->rchild=plr->lchild;
    p->lchild=plr->rchild;
    plr->lchild=pl;
    plr->rchild=p;

    p->height=nodeHeight(p);
    pl->height=nodeHeight(pl);
    plr->height=nodeHeight(plr);

    if(root==p) root=plr;
    return plr;
    
}
Node*RLrot(Node *p){
    Node *pr=p->rchild;
    Node *prl=pr->lchild;
    pr->rchild=prl->rchild;
    p->rchild=prl->lchild;
    prl->lchild=p;
    prl->rchild=pr;

    p->height=nodeHeight(p);
    pr->height=nodeHeight(pr);
    prl->height=nodeHeight(prl);

    if(root==p) root=prl;
    return prl;
}

Node* RInsert(Node *p, int key) {    
    Node *t=NULL;
    if (p == NULL){
        t=new Node;
        t->data=key;
        t->height=1;
        t->lchild=t->rchild=NULL;
        return t;
    }       
    if (key < p->data)
        p->lchild = RInsert(p->lchild, key);
    else if (key > p->data)
        p->rchild = RInsert(p->rchild, key);

    p->height=nodeHeight(p);

    if(balanceFactor(p)==2&&balanceFactor(p->lchild)==1)    return LLrot(p);
    if(balanceFactor(p)==-2&&balanceFactor(p->lchild)==-1)  return RRrot(p);
    if(balanceFactor(p)==2&&balanceFactor(p->lchild)==-1)   return LRrot(p);
    if(balanceFactor(p)==-2&&balanceFactor(p->lchild)==1)   return RLrot(p);    

    return p;
}
void InOrder(Node *p) {
    if (p != NULL) {       
        InOrder(p->lchild);
        cout << p->data << " ";
        InOrder(p->rchild);
    }
}
int main(){

    root=RInsert(root,10);
    RInsert(root,20);
    RInsert(root,30);
    RInsert(root,40);
    RInsert(root,50);
    RInsert(root,25);
    cout << "InOrder:";
    InOrder(root);   
    return 0;
}

