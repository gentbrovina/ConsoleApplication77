#include <iostream> 
#include <queue>
using namespace std;

class Node {
public:
    int data;
    Node* left;
    Node* right;

    Node() {
        left = NULL;
        right = NULL;
    }

    Node(int data) {
        left = NULL;
        right = NULL;
        this->data = data;
    }

};

int getLeafCount(Node* node)
{
    if (node == NULL)
        return 0;
    if (node->left == NULL && node->right == NULL)
    {
        return 1;
    }

        return getLeafCount(node->left) +
        getLeafCount(node->right);
}

bool printAncestors(Node* root, int target)
{
    if (root == NULL)
        return false;

    if (root->data == target)
        return true;

    if (printAncestors(root->left, target) ||
        printAncestors(root->right, target))
    {
        cout << root->data << " ";
        return true;
    }

}



int treeHeight(Node* root)
{
    if (root == NULL)
        return 0;

    queue<Node*> q;

    q.push(root);
    int height = 0;

    while (true)
    {
        int nodeCount = q.size();
        if (nodeCount == 0)
            return height;

        height++;

        while (nodeCount > 0)
        {
            Node* node = q.front();
            q.pop();
            if (node->left != NULL)
                q.push(node->left);
            if (node->right != NULL)
                q.push(node->right);
            nodeCount--;
        }
    }
}
int countNodes(Node* root)
{
    if (root == NULL)
        return (0);
    return (countNodes(root->left) + countNodes(root->right));
}

bool isComplete(Node* root, int index, int number_nodes)
{
    if (root == NULL)
        return (true);

    if (index >= number_nodes)
        return (false);

    return (isComplete(root->left, 2 * index + 1, number_nodes)
        && isComplete(root->right, 2 * index + 2, number_nodes));
}


Node* newNode(int data)
{
    Node* temp = new Node;
    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}


int main()
{
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->left->left->left = newNode(6);


    int node_count = countNodes(root);
    int index = 0;

    if (isComplete(root, index, node_count))
        cout << "Pema Binare eshte komplete. ";
    else
        cout << "Pema binare nuk eshte komplete. ";


    cout << "\nLartesia e pemes eshte: " << treeHeight(root);

    cout << "\nNumri i gjetheve te pemes eshte : " << getLeafCount(root) << endl;

    cout << "Nyjet paraardhese te nje nyje te caktuare jane: ";

    printAncestors(root, 6);


    return 0;
}
