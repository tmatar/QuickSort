# QuickSort
C++
/*quick sort algorithm */



#include <cstdlib> //necessary for general functions
#include <iostream>
#include <fstream> //necessary for inputting and outputting functions
using namespace std;

//this function prints out the array of numbers at each step of the iteration
void print_array(int array[], int low, int hi)
{
	cout<< "quick sort partition steps: ";
	for (int j=low; j<=hi;j++) //this for loop goes through the array and
		cout <<" "<< array[j]; //prints out each number
	cout << endl;
}//end of print_array

//this function swaps two elements in the array if one element is found to be
//smaller than the partition element
void swap (int arr[], int i, int j) //i & j are the two variables that are being compared
{
    int variable;       //introduced "int variable" to hold each element as they're being swapped

    variable = arr[i];
	arr[i] = arr[j];
	arr[j] = variable;

	return;
}

//this function chooses a pivot element and each time, it find an element less than or equal to the pivot
//this index is incremented and that element will be placed before the pivot (and that is when the swap function is called)
int partition (int arr[], int low, int hi)
{
	int pivot = arr[hi]; //initially, the last element in the array is chosen as the pivot
	int i = low;         //the counting index is set to 0

	for (int j = low; j<hi; j++)  //this for loop goes through the array of numbers and checks whether that element
	{                             //is less than or equal to the pivot & if it is, it will be placed before the pivot
		if (arr[j] <= pivot)
		{
			swap(arr, i, j);      //using this swap function
			i++;
		}
	}
	print_array(arr, low, hi);    //this prints the new array at each iteration
	swap(arr, i, hi);
	return i;
}

//this function calls in the partition function if the pivot element in the array is less than or equal to the number
//being compared
//else, it moves on to the next iteration
void quick_sort(int arr[], int low, int high)
{
	int pivot;

	if (low < high)
	{
		pivot = partition(arr, low, high); //calls the partition function if the if statement is true
		quick_sort(arr, low, pivot-1);     //this recursively runs the quicksort function on the element before the pivot
		quick_sort(arr, pivot+1, high);    //this recursively runs the quicksort function on the element after the pivot
	}

	return;
}

	int main()
	{
		int MAX_LENGTH;
		int i;
		MAX_LENGTH = 200; //maximum number of elements in an array

        //this is the array being declares
		int array[MAX_LENGTH] = {'\0'};

		//declare and intialise input and output pipes
        ifstream inFile;

        //opens the input file
        inFile.open("input.txt");

        //reads the numbers in the file into the array
        //set to stop at the end of the file
        for(i = 0; i<MAX_LENGTH && !inFile.eof(); i++)
		{
				inFile >> array[i];
		}

		print_array(array, 0, i-2); //prints the array before sorting
		quick_sort(array, 0, i-2);  //sorts the numbers in the array
		print_array(array, 0, i-2); //prints the numbers after sorting

		inFile.close(); //closes input file pipe

		return 0;

	}//end of main

