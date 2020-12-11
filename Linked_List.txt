#include<iostream>
#include<conio.h>
using namespace std;

class Node {
public:
	int key; // key is the Unique ID of every NOde
	int data;  
	Node* next; // address of next node
	
	Node() // default Constructor
	{
		key = 0;
		data = 0;
	}
	Node(int k, int d)// perametaraize constructor
	{
		key = k;
		data = d;
	}
};

class Linked_list {
public:
	Node* head; // To store the address of head node of Linked list

	Linked_list()
	{
		head = NULL;
	}
	Linked_list(Node* n)
	{
		head = n;
	}
	Node* nodeExists(int k)// it will check that the key exists or not, if yes then it will return node address
	{
		Node* temp = NULL;
		Node* ptr = head;
		while (ptr != NULL) // head is NULL, only when no Node is attached to it.
		{
			if (ptr->key == k)
			{
				temp = ptr; 
			}
			ptr = ptr->next; // (like Increment) it will change the ptr pointer from current node to another node
		}
		return temp;
	}



	void append_node(Node* n)// it will add a node at the end of the list
	{
		if (nodeExists(n->key) != NULL)// check if key already exist
		{
			cout << "Node is Already Exist with same key..." << endl;
		}
		else
		{
			if (head == NULL)// head is NULL, when thare is no NOde in the linked list
			{
				head = n;
				cout << "Node Appended" << endl;
			}
			else
			{
				Node* ptr = head; // we have traverse through whole list to find the last node, so we need address of head to start form
				while (ptr->next != NULL) // when next address of ptr is NULL, so it means that there is no node attached to this 
				{
					ptr = ptr->next; 
				}
				ptr->next = n; // ptr have the address of last node, so we point the Next of last node to New node 'n'
				cout << "Node Appended" << endl;
			}

		}

	}


	void prepand_node(Node* n)
	{
		if (nodeExists(n->key) != NULL)// check if key already exist
		{
			cout << "Node is Already Exist with same key..." << endl;
		}
		else
		{
			n->next = head; // as we know that head has the address of first node of list so we make a node and the address of Next of new node is pointed to head
			head = n; // as we created new node in the start of list so the head will change to new node n
		}



	}


	void insert_node(int k, Node* n)
	{
		Node* ptr = nodeExists(k);// check key
		if (ptr == NULL)
		{
			cout << "No node Exist with entered key" << endl;

		}
		else
		{
			if (nodeExists(n->key) != NULL)// check if key of new node already exist
			{
				cout << "Node is Already Exist with same key..." << endl;
			}
			else
			{
				n->next = ptr->next; // "Next of n" will store same address which "Next of ptr" is storing, ptr is storing the address of given key from line 99
				ptr->next = n; // and ptr of next will store the current address of new node
			}
		}
	}


	void delete_node(int k)
	{
		if(head == NULL)
		{
			cout << "No node exist" << endl;
		}
		else if (head != NULL)
		{
			if (head->key == k)// if the enterd key is the key of head 
			{
				head = head->next;//  then the head pointer will shift pointing towards the next of head
				cout << "NOde Deleted" << endl;
			}
			else
			{
				Node* temp = NULL;
				Node* prev = head;
				Node* next_ptr = head->next;
				while (next_ptr != NULL)// loop will execute until the next ptr is equal to NULL
				{

					if (next_ptr->key == k)// if the key value store in the next ptr which is next of head then it means that delete this node
					{
						temp = next_ptr;// it will store the address of node which is to delete
						next_ptr = NULL;// when it equals to NULL then the loop will exit
					}
					else
					{
						prev = prev->next; // to change the pointer possition
						next_ptr = next_ptr->next;// change the pointer posstion
					}
				}
				if (temp != NULL)
				{
					prev->next = temp->next; // in A,B,C Node we have to delete A node then prev have the address of A,
												// temp have the address of B, A(next) have address of B, and B(next) have address of B
											// to delete B node we will assign the address of C (stored in B(next) ) to next of A(next of prev)
											// which will replace address of B stroed in A(next) by Address of C.
					cout << "Node Deleted ..." << endl;
				}
				else
				{
					cout << "Node doesn't exist with entered key value" << endl;
				}

			}
		}

	}


	void update_data(int k, int d)
	{
		Node* ptr = nodeExists(k);// check if the node exist with key or not
		if (ptr != NULL)// if node exist then ptr have address of that node
		{
			ptr->data = d;
			cout << "Data updated Sucessfully" << endl;
		}
		else
		{
			cout << "Node not found with entered key" << endl;
		}
	}

	void print_list()
	{
		if (head == NULL)
		{
			cout << "Linked list is Empty.." << endl;
		}
		else
		{
			cout << "DAta on Linked List..." << endl;;
			Node* temp = head;
			while (temp->next != NULL)
			{
				cout << "Key = " << temp->key << " , Data = " << temp->data << endl;
				temp = temp->next;
			}

		}
	}

};

int main()
{
	Linked_list S;
	int option;
	int key1, k1, data;
	while (true)
	{

		cout << "1 = Append Node" << endl;
		cout << "2 = Prepend Node" << endl;
		cout << "3 = Insert Node at Loction" << endl;
		cout << "4 = Delete Node " << endl;
		cout << "5 = Updata Node data" << endl;
		cout << "6 = Print data of node" << endl;
		cout << "Enter Choice = ";
		cin >> option;
		Node* N = new Node();// Dynammic Memory Allocation
		
		
		switch (option)
		{
		case 1:
			cout << "Append Operation" << endl;
			cout << "Enter Key = ";
			cin >> key1;
			cout << "Enter Data = ";
			cin >> data;
			N->key = key1;
			N->data = data;
			S.append_node(N);

			break;
			
		case 2:
			cout << "Prepend Operation" << endl;
			cout << "Enter Key = ";
			cin >> key1;
			cout << "Enter DAta = ";
			cin >> data;
			N->data = data;
			N->key = key1;
			S.prepand_node(N);
			break;
			
		case 3:
			cout << "Insert Node at specific Location" << endl;
			cout << "Enter Key after you want to insert new node = ";
			cin >> k1;
			cout << "Enter Key of New Node = ";
			cin >> key1;
			cout << "Enter Data of New node = ";
			cin >> data;
			N->data = data;
			N->key = key1;
			S.insert_node(k1, N);
			break;

		case 4:
			cout << "Delete Node Operatioin" << endl;
			cout << "Enter Key of Node to Delete = ";
			cin >> k1;
			S.delete_node(k1);
			break;
			
		case 5:
			cout << "Update Node Operation" << endl;
			cout << "Enter Key of Node = ";
			cin >> key1;
			cout << "Enter New Data = ";
			cin >> data;
			S.update_data(key1, data);
			break;
			
		case 6:
			S.print_list();
				break;
			
		default:
			cout << "Invalid Option Selected" << endl;

		}

		_getch();
		system("cls");
	}


	
	system("pause");
}



