# C-C-
//qsort
#include<stdlib.h>
#include<string.h>

void Swap(char*buf1, char*buf2, int width)
{
	int i = 0;
	for (i = 0; i < width; i++)
	{
		char tmp = *buf1;
		*buf1 = *buf2;
		*buf2 = tmp;
		buf1++;
		buf2++;
	}
}

int int_cmp(const void* e1, const void* e2)
{
	return *(int*)e1 - *(int*)e2;
}

void bubble_sort(void* base, int sz, int width, int(*cmp)(void* e1, void* e2))
{
	int i = 0;
	//趟数
	for (i = 0; i < sz - 1; i++)
	{
		int j = 0;
		//每一趟比较的次数
		for (j = 0; j < sz - 1 - i; j++)
		{
			//两个元素的比较
			if (cmp((char*)base + j * width, (char*)base + (j + 1) * width) > 0)
			{
				//交换
				Swap((char*)base + j * width, (char*)base + (j + 1) * width, width);
			}
		}
	}
}

void test1()
{
	int i = 0;
	int arr[] = {8,7,6,5,4,3,2,1,0};
	int sz = sizeof(arr) / sizeof(arr[0]);
	bubble_sort(arr, sz, sizeof(arr[0]), int_cmp);
	//qsort(arr, sz, sizeof(arr[0]), int_cmp);
	for (i = 0; i < sz; i++)
	{
		printf("%d ", arr[i]);
	}
	printf("\n");
}

int float_cmp(const void* e1, const void* e2)
{
	if (*(float*)e1 == *(float*)e2)
		return 0;
	else if (*(float*)e1 > *(float*)e2)
		return 1;
	else
		return -1;
}

void test2()
{
	int i = 0;
	float f[] = { 8.0,9.0,7.0,6.0,5.0,4.0,2.0,3.0,1.0 };
	int sz = sizeof(f) / sizeof(f[0]);
	//qsort(f, sz, sizeof(f[0]), float_cmp);
	bubble_sort(f, sz, sizeof(f[0]), float_cmp);
	for (i = 0; i < sz; i++)
	{
		printf("%f ", f[i]);
	}
	printf("\n");
}

struct Stu
{
	char name[20];
	int age;
};

int Stu_cmp_by_age(const void* e1, const void* e2)
{
	return ((struct Stu*)e1)->age - ((struct Stu*)e2)->age;
}

void test3()
{
	int i = 0;
	struct Stu s[3] = { {"chenle",21},{"jisung",20},{"mark",22} };
	int sz = sizeof(s) / sizeof(s[0]);
	//qsort(s, sz, sizeof(s[0]), Stu_cmp_by_age);
	bubble_sort(s, sz, sizeof(s[0]), Stu_cmp_by_age);
	for (i = 0; i < sz; i++)
	{
		printf("%s ", s[i].name);
	}
	printf("\n");
}

int Stu_cmp_by_name(const void* e1, const void* e2)
{
	return strcmp(((struct Stu*)e1)->name, ((struct Stu*)e2)->name);
}

void test4()
{
	int i = 0;
	struct Stu s[3] = { {"chenle",21},{"jisung",20},{"mark",22} };
	int sz = sizeof(s) / sizeof(s[0]);
	qsort(s, sz, sizeof(s[0]), Stu_cmp_by_name);
	bubble_sort(s, sz, sizeof(s[0]), Stu_cmp_by_name);
	for (i = 0; i < sz; i++)
	{
		printf("%s ", s[i].name);
	}
	printf("\n");
}

int main()
{
	test1();
	test2();
	test3();
	test4();
}
