# veriyap-lar-
Birinci soru:
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define SIZE 500

void insertionSort(int arr[]) {
    int i, key, j;
    for (i = 1; i < SIZE; i++) {
        key = arr[i];
        j = i - 1;

        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

void selectionSort(int arr[]) {
    int i, j, min_idx, temp;

    for (i = 0; i < SIZE - 1; i++) {
        min_idx = i;
        for (j = i + 1; j < SIZE; j++) {
            if (arr[j] < arr[min_idx])
                min_idx = j;
        }

        temp = arr[min_idx];
        arr[min_idx] = arr[i];
        arr[i] = temp;
    }
}

int main() {
    int arr1[SIZE], arr2[SIZE];
    int i;

    srand(time(NULL));

    for (i = 0; i < SIZE; i++) {
        int num = rand() % 1001;
        arr1[i] = num;
        arr2[i] = num;
    }

    clock_t start, end;

    start = clock();
    insertionSort(arr1);
    end = clock();
    double time1 = (double)(end - start) / CLOCKS_PER_SEC;

    start = clock();
    selectionSort(arr2);
    end = clock();
    double time2 = (double)(end - start) / CLOCKS_PER_SEC;

    printf("Insertion Sort Süresi: %f saniye\n", time1);
    printf("Selection Sort Süresi: %f saniye\n", time2);

    return 0;
}

İkinci soru:
#include <stdio.h>

#define SIZE 6

void ozelSirala(int arr[]) {
    int i, j, temp;

    // Önce diziyi küçükten büyüğe sırala (Bubble Sort)
    for (i = 0; i < SIZE - 1; i++) {
        for (j = 0; j < SIZE - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }

    int sonuc[SIZE];
    int left = 0;
    int right = SIZE - 1;
    int k = 0;

    while (left <= right) {
        sonuc[k++] = arr[right--];
        if (left <= right)
            sonuc[k++] = arr[left++];
    }

    printf("Yeni sıralama: ");
    for (i = 0; i < SIZE; i++) {
        printf("%d ", sonuc[i]);
    }
}

int main() {
    int dizi[SIZE] = {60, 80, 3, 9, 57, 11};

    ozelSirala(dizi);

    return 0;
}

Üçüncü soru:
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define ALPHABET_SIZE 26

typedef struct TrieNode {
    struct TrieNode *children[ALPHABET_SIZE];
    int isEndOfWord;
} TrieNode;

TrieNode* createNode() {
    TrieNode* node = (TrieNode*)malloc(sizeof(TrieNode));
    node->isEndOfWord = 0;

    for (int i = 0; i < ALPHABET_SIZE; i++)
        node->children[i] = NULL;

    return node;
}

void insert(TrieNode* root, char* key) {
    TrieNode* temp = root;

    for (int i = 0; key[i] != '\0'; i++) {
        int index = key[i] - 'a';

        if (!temp->children[index])
            temp->children[index] = createNode();

        temp = temp->children[index];
    }

    temp->isEndOfWord = 1;
}

int search(TrieNode* root, char* key) {
    TrieNode* temp = root;

    for (int i = 0; key[i] != '\0'; i++) {
        int index = key[i] - 'a';

        if (!temp->children[index])
            return 0;

        temp = temp->children[index];
    }

    return temp->isEndOfWord;
}

int main() {
    TrieNode* root = createNode();

    insert(root, "cat");
    insert(root, "car");
    insert(root, "dog");

    printf("cat: %d\n", search(root, "cat"));
    printf("car: %d\n", search(root, "car"));
    printf("dog: %d\n", search(root, "dog"));
    printf("cow: %d\n", search(root, "cow"));

    return 0;
}
