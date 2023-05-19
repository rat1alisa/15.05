# 15.05

#include <iostream>
using namespace std;

template <typename T>
class List
{
public:
    List();
    ~List();
    
    void push_back(T data);//удаление переднего элемента
    int GetSize () { return Size; };
    void pop_front();
    void clear();
    void push_front(T data);
    void insert(T value, int index);
    void removeAd(int index);
    
    T& operator[](const int index);
    
private:
    
    template <typename T>
    class Node //1 элемент
    {
    public:
        Node *pNext;//указатель на следующий элемент
        T data;
        Node (T data = T(), Node *pNext = nullptr)
        {
            this -> data = data;
            this -> pNext = pNext;
        }
    };
    int Size;
    Node<T> *head;
    
};

template <typename T>
List<T>::List()//конструктор
{
    Size = 0;//кол-во элементов
    head = nullptr;//нулевой элемент
}

template <typename T>
List<T>::~List()//деструктор
{
    cout << "Destructor called";
    clear();
}

template <typename T>
List<T>::pop_front()
{
    Node<T> *temp = head;
	head = head->pNext;
	
	delete temp;
	Size--;
}

template <typename T>
void List<T>::push_back(T data)
{
    if (head == nullptr)
    {
        head = new Node<T>(data);
    }
    else
    {
        Node<T> *current = this->head;
        
        while(current -> pNext != nullptr)
        {
            current = current->pNext;
        }
        current-> pNext = new Node<T>(data);
    }
    Size++;
}

template <typename T>
void List<T>::clear()//удаление всех элементов
{
    while (Size)
	{
		pop_front();
	}
}

template <typename T>
T & List<T>::operator[](const int index)
{
    int counter = 0;
	Node<T> *current = this->head;
	while (current != nullptr)
	{
		if (counter == index)
		{
			return current->data;
		}
		current = current->pNext;
		counter++;
	}
}

template <typename T>
void List<T>::push_front(T data)//добавление вперед
{
    cout << "Enter new element - ";
	cin >> data;
    head = new Node<T>(data,head);
    Size++;
}

template <typename T>
void List<T>::insert(T data)
{
    cout << "Enter element index - ";
	cin >> index;
	cout << "Enter element data - ";
	cin >> data;
	if (index == 0)
	{
		push_front(data);
	}
	else
	{
		Node<T>* previous = this->head;
		for (int i = 0; i < index-1; i++) 
		{
			previous = previous->pNext;
		}
		Node<T>* newNode = new Node<T>(data);
		previous->pNext = newNode;
		Size++;
	}
}

template <typename T>
void List<T>::removeAd(T data,int index)
{
	cout << "Enter index -";
	cin >> index;
	if (index == 0)
	{
		pop_front();
	}
	else
	{
		Node<T>* previous = this->head;
		for (int i = 0; i < index - 1; i++)
		{
			previous = previous->pNext;
		}
		Node<T>* toDelete = previous->pNext;
		previous->pNext = toDelete->pNext;
		delete toDelete;
		Size--;
	}
}
//---------------------------------------
int main()
{
    setlocale(LC_ALL, "RU");
    srand(time(NULL));
	List<int>lst;
	int ch;
	cout << "\tHEADER" << endl;
	cout << "1. Add to the end\n";
	cout << "2. Add to the front\n";
	cout << "3. Add element index\n";
	cout << "4. Delete element by index\n";
	cout << "5. List size\n";
	cout << "6. Delete element\n";
	cout << "7. Delete list\n";
	cout << "8. Print list\n";
	cout << "9. Other\n";
	do {
		cin >> ch;
		switch (ch) 
		{
		case 1: (ch == 1);
		{
			lst.push_back(2);
			break;
		}
		case 2: (ch == 2);
		{
			lst.push_front(2);
			break;
		}
		case 3: (ch == 3);
		{
			lst.insert(1, 2);
			break;
		}
		case 4: (ch == 4);
		{
			lst.removeAd(2);
			break;
		}
		case 5: (ch == 5);
		{
			cout << "List Size - " << lst.GetSize() << endl;
			break;
		}
		case 6: (ch == 6);
		{
			lst.pop_front();
			cout << "The first element has been removed\n";
			break;
		}
		case 7: (ch == 7);
		{
			lst.~List();
			break;
		}
		case 8: (ch == 8);
		{
			cout << "List: "; 
			for (int i = 0; i < lst.GetSize(); i++)
			{
				cout << lst[i] << ' | ';
			}
			cout << endl << endl;
			break;
		}
		case 9: (ch == 9);
		{
			break;
		}
		default:
		{
			cout << "ERROR";
		}
		}
	} while (ch != 9);
	system("pause");
	return 0;
}
