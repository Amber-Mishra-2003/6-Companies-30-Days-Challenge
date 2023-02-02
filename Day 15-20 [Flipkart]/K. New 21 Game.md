# New 21 Game

Problem Link :- [Link]()

<h3>
Problem :- Alice plays the following game, loosely based on the card game "21".

Alice starts with 0 points and draws numbers while she has less than k points. During each draw, she gains an integer number of points randomly from the range [1, maxPts], where maxPts is an integer. Each draw is independent and the outcomes have equal probabilities.

Alice stops drawing numbers when she gets k or more points.

Return the probability that Alice has n or fewer points.

Answers within 10-5 of the actual answer are considered accepted.
</h3>


**Solution :-**
```
class Solution {
public:
    double new21Game(int N, int K, int W) {
        
        if (K == 0) return 1;
        double prob[K + W], prob_sum = 1, cnst = (1.0 / W);
        prob[0] = 1.0;
        queue<int> q;
        q.push(0);
        
        for(int i = 1; i < K + W; i++)
        {
            while(q.front() < i - W)
            {
                prob_sum -= prob[q.front()];
                q.pop();
            }
            prob[i] = prob_sum * cnst;
            if(i < K)
            {
                q.push(i);
                prob_sum += prob[i];
            }
        }
        
        double numr = 0, denr = 0;
        for(int i = K; i < K + W; i++)
        {
            denr += prob[i];
            if (i <= N) 
                numr += prob[i];
        }
        
        return numr / denr;
    }
};
```
