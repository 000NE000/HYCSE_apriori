# HYCSE_apriori
## data load
>load_data(input_path)
- file open
	- main.py에서 CLI args parsing한 후, 해당 input file name을 받아서
- reading data
- converting each line to item set
## Frequent Pattern 생성; apriori
#### `make_next_candidate(prev_frequent)`
###### 새로운 candidate (length k+1)를 만들 때 고려해야 하는 상황
- **Condition 1:** 
	- They must share exactly k-1 elements.

- **Condition 2:** 
	- Let the unique element from A be a and from B be b. In order to include the union $\{a,b\} \cup (A \cap B)$ in your new set list (of length k+1), there must already be a set in your input l that contains both a and b.
	- I can implement this by sorting and comparing
#### `prune_step(candidates, prev_frequent)`
##### parameter
- candidates : k+1 크기의 candidate
- prev_frequent : k 크기의 freq. pattern
###### 핵심 로직
- k+1 크기의 candidate에 대해, k 크기의 subset을 뽑았다고 할 때 모든 것들이 Prev_frequent에 속해야 함.
- apriori의 핵심 : Any subset of a frequent itemset must be frequent

#### `apriori(transactions, min_support)`
> support계산시 `get_support`함수를 이용
###### 1st. k=1인 후보 만들고 각각의 support 계산
###### 2nd. k >= 2에 대해 `make_next_candidate`와`prune_step`을 이용해 모든 후보를 생성 

## confidence 계산하기
#### `generate_association_rules(freq_patterns)`
###### implement : 어떻게 disjoint한 두 부분집합을 구할 것인가
For each closed pattern s (with support) generate all association rules of the form:
 A -> (s - A)
for every nonempty proper subset A of s.
Returns a list of tuples: (antecedent, consequent, support(s), confidence)
- compute confidence
	- Choose two subsets of selected closed pattens which are disjoint
	- Compute confidence
	- $\text{Confidence}(X \Rightarrow Y) = \frac{\text{Support}(X \cup Y)}{\text{Support}(X)}$
#### `proper_noempty_subsets(s)`
Return list of subset of s which is not null set

---
##### environment requirement
- 3.12.9 | packaged by Anaconda, Inc. | (main, Feb  6 2025, 12:55:12) [Clang 14.0.6 ]
- List dependency
	- 아래 코드의 실행 결과가 requirements.txt에 저장됨
``` 
pip freeze > requirements.txt
```

![[Pasted image 20250324012225.png]]
