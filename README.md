#include <stdio.h>
#include <stdlib.h>

// Define the structure for a binary tree node
struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

// Function to create a new node
struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    if (newNode == NULL) {
        printf("Memory allocation failed!\n");
        exit(1);
    }
    newNode->data = data;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

// Pre-order Traversal: Root -> Left -> Right
void preorderTraversal(struct Node* root) {
    if (root == NULL) return;
    printf("%d ", root->data);
    preorderTraversal(root->left);
    preorderTraversal(root->right);
}

// In-order Traversal: Left -> Root -> Right
void inorderTraversal(struct Node* root) {
    if (root == NULL) return;
    inorderTraversal(root->left);
    printf("%d ", root->data);
    inorderTraversal(root->right);
}

// Post-order Traversal: Left -> Right -> Root
void postorderTraversal(struct Node* root) {
    if (root == NULL) return;
    postorderTraversal(root->left);
    postorderTraversal(root->right);
    printf("%d ", root->data);
}

// Function to free memory allocated for the tree
void freeTree(struct Node* root) {
    if (root == NULL) return;
    freeTree(root->left);
    freeTree(root->right);
    free(root);
}

int main() {
    /* 
       Manually creating a structured binary tree:
                 1
               /   \
              2     3
             / \
            4   5
    */
    
    // Create the root node
    struct Node* root = createNode(1);
    
    // Create children
    root->left = createNode(2);
    root->right = createNode(3);
    
    // Create grandchildren
    root->left->left = createNode(4);
    root->left->right = createNode(5);

    // Display traversals
    printf("Pre-order traversal:  ");
    preorderTraversal(root);
    printf("\n");

    printf("In-order traversal:   ");
    inorderTraversal(root);
    printf("\n");

    printf("Post-order traversal: ");
    postorderTraversal(root);
    printf("\n");

    // Clean up memory
    freeTree(root);

    return 0;
}
