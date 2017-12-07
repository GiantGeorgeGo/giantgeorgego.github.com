---
layout: default 
title: Introduce two methods of calculate triple sum equal zero question
---
{% include JB/setup %}

<i>The triple sum problem</i>

   Given an array S of n integers, are there elements a, b, c in S 
   such that a + b + c = 0? Find all unique triplets in the array
   which gives the sum of zero.
   Note: The solution set must not contain duplicate triplets.
   For example, given array S = [-1, 0, 1, 2, -1, -4],
   A solution set is:
     [
       [-1, 0, 1],
       [-1, -1, 2]
      ]

//N^2 * logN number of 3sum 0 = 70 - better time spent = 0.029919s
int tri_sum_better(int data[], int size) {
  int ret = 0;

  bubble_sort(data, size);

  for (int i = 0; i <= size - 1; ++i) {
    for (int j = i + 1; j <= size - 1; ++j) {
      int ij = data[i] + data[j];
      int res = binary_search(data, 0, size - 1, -ij);
      if (res != i && res != j && -1 != res) {
        ++ret;
      }
    }
  }

  return ret / 3;
}

//N^3   number of 3sum 0 = 70 - time spent = 0.361940s
int tri_sum_brute(int data[], int size) {
  int ret = 0;
  for (int i = 0; i < size; ++i) {
    for (int j = i + 1; j < size; ++j) {
      for (int k = j + 1; k < size; ++k) {
        if (0 == data[i] + data[j] + data[k]) {
          ++ret;
        }
      }
    }
  }

  return ret;
}

int main(int argc, char** argv) {
  if (2 != argc) {
    pf("Only the input file path is needed");
    return -1;
  }
  int i = 0;
  int fd = open_file(argv[1]);
  size_t file_size = get_file_size(argv[1]);

  clock_t start, end;

  if (0 == file_size) return 0;

  char* sample = (char*)malloc(file_size * sizeof(char));
  int num_sample = read(fd, sample, file_size * sizeof(char));
  int num_data = num_sample >> 3;
  pf("num read sample %d", num_sample);

  for (i = 0; i < num_data; ++i) {
    sample[i * 8 + 7] = '\0';
  }

  int data[num_data];
  for (i = 0; i < num_data; ++i) {
    data[i] = StrToInt(sample + i * 8);
  }

  start = clock();
  int sum3equal0 = tri_sum_brute(data, num_data);
  end = clock();

  pf("number of 3sum 0 = %d - brute time spent = %fs",
     sum3equal0, (double)(end - start) / CLOCKS_PER_SEC);

  start = clock();
  int sum3equal1 = tri_sum_better(data, num_data);
  end = clock();

  pf("number of 3sum 0 = %d - better time spent = %fs",
     sum3equal1, (double)(end - start) / CLOCKS_PER_SEC);

  delete sample;
  close(fd);

  return 0;
}
8. Source code on github:  
           [Code](https://github.com/GiantGeorgeGo/data-struct-and-algorithm/blob/master/3sum0.c).


<p>{{ page.date | date_to_string }}</p>
