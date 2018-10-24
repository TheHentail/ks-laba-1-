// Lab03.cpp : Defines the entry point for the console application.
//Стэк

#include "stdafx.h"
#include <iostream>
#include <ctime>

using namespace std;
					//---Декларация структурного типа---//
struct Stack {      //
	int info;		//
	Stack* next;	//
};  		//
								//---Декларация прототипов функций пользователя---//
Stack* InStack(Stack*, int);	// Функция формирования элементов стека		
void View(Stack*);				// Функция просмотра информации стека		
void Del_All(Stack**);			// Функция очистки памяти					
void Sort_p(Stack **p);			// Функция сортировки информации стека		
void search(Stack* begin);			// Функция удаления максимального элемента


int main()
{
	Stack *t=NULL;
	int i, in, n, kod;
	Stack *begin = NULL;
	while (true) {
		cout << "\n\tCreate - 1.\n\tAdd    - 2.\n\tView   - 3.\n\tDel    - 4.\n\tSort    -5\n\tTask    -6\n\tEXIT   - 0.\n\t";
		cin >> kod;
		switch (kod) {
		case 1: case 2:
			if (kod == 1 && begin != NULL) {			//Если создаем новый стек, должны освободить память, занятую предыдущим
				cout << "Clear Memory first!" << endl;
				break;
			}
			cout << "Input kol = "; cin >> n;
			srand(time(0));
			for (i = 1; i <= n; i++) {
				in = rand() % 100 -30;					//Заполняем информационную часть случайными числами от -30 до 100
				begin = InStack(begin, in);
			}
			if (kod == 1) cout << "Create " << n << endl;
			else cout << "Add " << n << endl;
			break;
		case 3:
			if (!begin) {
				cout << "Stack Is Empty!" << endl;
				break;
			}
			cout << "--Stack--" << endl;
			View(begin);
			break;
		case 4:
			Del_All(&begin);
			cout << "Memory Free!" << endl;
			break;
		case 5: 
			if (begin != NULL) {
				Sort_p(&begin);
				cout << "Stack Sorted!" << endl;
			}
			else cout << "Stack is Empty!" << endl;
			break;
		case 6:
			if (begin == NULL) {
				cout << "Stack is Empty!" << endl;
				break;
			}
			search(begin);
			cout << "--Task 4--" << endl;
			break;
		case 0: 
			if (begin != NULL)
				Del_All(&begin);
			return 0;					  //Выход (EXIT)
		}
	}
    return 0;
}

//---Функция добавления элемента в стек---//
Stack* InStack(Stack *p, int in) {		  //
	Stack *t = new Stack;				  //Захват памяти для элемента
	t->info = in;						  //Формируем информационную часть
	t->next = p;						  //Формируем адресную часть
	return t;
}

//---Функция просмотра стека---//
void View(Stack *p){
	Stack *t = p;
	while (t != NULL) {
		cout << t << " " << t->info << " " << t->next << endl;	  //Вывод на экран информационной части
		t = t->next;
	}
}

//---Функция освобождения памяти--//
void Del_All(Stack **p) {
	while (*p != NULL) {
		t = *p;
		*p = (*p)->next;
		delete t;
	}
}

//--Функция сортировки информации стека--//
void Sort_p(Stack **p) {
	Stack *t = NULL, *t1, *r;
	if ((*p)->next->next == NULL) return;
	Stack *u = new Stack;
	int as=12
	u->info = as;
	u->next = *p;
	do {
		for (t1 = *p; t1->next->next != t; t1 = t1->next)
			if (t1->next->info  >  t1->next->next->info) {
				r = t1->next->next;
				t1->next->next = r->next;
				r->next = t1->next;
				t1->next = r;
			}
		t = t1->next;
	} while ((*p)->next->next != t);
	//Stack *u = NULL;
	//u = *p;
	//*p = *p->next;
	//delete u;
}
 	
void search(Stack* begin)
{
	Stack* temp = begin;
	Stack* max = begin;
	Stack* prevMax = NULL;
	while (temp->next)
	{
		if (temp->next->info > max->info)
		{
			prevMax = temp;
			max = temp->next;
		}
		temp = temp->next;
	}
	// Удаляем
	Stack* del = prevMax->next;
	prevMax->next = prevMax->next->next;
	delete del;
		}

	
