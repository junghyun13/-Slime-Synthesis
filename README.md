# -Slime-Synthesis
# The first line is given the number of test cases T , followed by T test cases. The first line of each test case is given the number of slimes N (1 ≤ N ≤ 60), and the second line is given N natural numbers. To synthesize a slime with A slime energy and a slime with B slime energy, A × B electrical energy is required. Print the remainder of dividing by 1,000, 000, 007 the minimum cost to be charged when you synthesize each slime to the end! 첫 번째 줄에 테스트 케이스의 수 T 가 주어지고, 이어서 T 개의 테스트 케이스가 주어진다. 각 테스트 케이스의 첫 번째 줄에는 슬라임의 수 N (1 ≤ N ≤ 60)이 주어지고, 두 번째 줄에는 N 개의 자연수가 주어진다.  A만큼의 슬라임 에너지를 가진 슬라임과 B만큼의 슬라임 에너지를 가진 슬라임을 합성하려면 A × B 만큼의 전기 에너지가 필요한데 각 합성 단계마다 필요한 전기 에너지들을 모두 곱한값이 최소가 되도록 합성해야하는데 각 테스트 케이스마다 슬라임을 끝까지 합성했을 때 청구될 비용의 최솟값을 1, 000, 000, 007로 나눈 나머지를 출력해라!
# 그리디 알고리즘
그리디(Greedy) 알고리즘은 탐욕법이라고도 하며, 현재 상황에서 지금 당장 좋은 것만 고르는 방법을 의미합니다.
일반적인 그리디 알고리즘은 문제를 풀기 위한 최소한의 아이디어를 떠올릴 수 있는 능력을 요구합니다.
그리디 알고리즘을 이용하면 매 순간 가장 좋아 보이는 것만 선택하며, 현재의 선택이 나중에 미칠 영향에 대해서는 고려하지 않습니다.
예시) 동전 최소 개수 구하기 
n = 1260
count = 0
# 큰 단위의 화폐부터 차례대로 확인하기
coin_types = [500, 100, 50, 10]
for coin in coin_types:
    count += n // coin # 해당 화폐로 거슬러 줄 수 있는 동전의 개수 세기
    n %= coin
print(count) #result--> 6
# python
# case 1:
import heapq, sys
input = sys.stdin.readline
for tc in range(int(input())):
    n = int(input())
    slime = []
    for x in list(map(int, input().split())):
        heapq.heappush(slime, x)   
    energy = 1
    while len(slime) != 1:
        x1 = heapq.heappop(slime)
        x2 = heapq.heappop(slime)
        new_slime = x1 * x2
        heapq.heappush(slime, new_slime)
        energy = energy * (new_slime % 1000000007)
        energy %= 1000000007
    print(energy % 1000000007)
# case 2:
import sys
import heapq
input = sys.stdin.readline
for _ in range(int(input())):
    N = int(input())
    slime = [*map(int, input().split())]
    heapq.heapify(slime)
    result = 1
    p = 1000000007
    while len(slime) > 1:
        s1 = heapq.heappop(slime)
        s2 = heapq.heappop(slime)
        result *= s1*s2 % p
        heapq.heappush(slime, s1*s2)
    print(result % p)
#input--> 2  5  3 10 2 8 14  1  13
#result-->271950400 1
