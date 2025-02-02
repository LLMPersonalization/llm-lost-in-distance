<div id="user-content-toc">
  <ul align="center" style="list-style: none;">
    <summary>
      <h1>Lost-in-Ditance in LLMs</h1>
    </summary>
  </ul>
  <ul align="center" style="list-style: none;">
    <summary>
      <a href='https://arxiv.org/pdf/2410.01985'>Paper Link</a> :eyes:
    </summary>
  </ul>  
</div>

## 1. What is Lost-in-Distance
LLM performance in graph tasks that exceed simple “needle-in-a-haystack” scenarios—where the solution involves cross-referencing and reasoning across multiple subproblems simultaneously—is heavily influenced by how closely relevant information is positioned within the context. We describe this effect as “lost-in-distance,” highlighting how the scattered placement of critical data can impede the model’s ability to reason and arrive to the correct result.

## 2. Example of the Model Input Prompt
<div style="background-color: #f3f3f3; padding: 1em;">
  <table style="width:100%; border-collapse: collapse;" border="1">
    <tr>
      <th>Prompt</th>
      <th>Answer (GPT-4o)</th>
    </tr>
    <tr>
      <td>
        You are given an undirected graph structure in an adjacency list format.<br><br>
        Given three nodes i, j, and k, your task is to determine if the number of common connections between node i and node j is greater than the number of common connections between node j and node k.<br><br>
        You MUST first answer several subquestions in '&lt;sub q&gt;&lt;/sub q&gt;' tags in order and put your answers in '&lt;sub a&gt;&lt;/sub a&gt;' tags in order. Finally, answer the question in the '&lt;final q&gt;&lt;/final q&gt;' tag based on the given graph and your answers to the subquestions. Put your final answer in the '&lt;final a&gt;&lt;/final a&gt;' tag.<br><br>
        In this graph:<br>
        Node 963 is connected to nodes {neighbors of node 963}.<br>
        Node 452 is connected to nodes {neighbors of node 452}.<br>
        Node 423 is connected to nodes {neighbors of node 423}.<br><br>
        &lt;sub q&gt;What are the unique common connections between node 963 and node 452? Your answer MUST start with 'The unique common connections between node 963 and node 452 are'.&lt;/sub q&gt;<br>
        &lt;sub q&gt;How many common connections are there between node 963 and node 452? Your answer MUST be a number only.&lt;/sub q&gt;<br>
        &lt;sub q&gt;What are the unique common connections between node 452 and node 423? Your answer MUST start with 'The unique common connections between node 452 and node 423 are'.&lt;/sub q&gt;<br>
        &lt;sub q&gt;How many common connections are there between node 452 and node 423? Your answer MUST be a number only.&lt;/sub q&gt;<br><br>
        &lt;final q&gt;Based on the given graph and previous answers, is the number of common connections between node 963 and node 452 greater than the number of common connections between node 452 and node 423? Your answer MUST be 'Yes' or 'No' only.&lt;/final q&gt;
      </td>
      <td>
        &lt;sub a&gt;The unique common connections between node 963 and node 452 are 704, 799, 972, 430, 827, 531, 628, 496, 551, 908, 104.&lt;/sub a&gt;<br>
        &lt;sub a&gt;11&lt;/sub a&gt;<br>
        &lt;sub a&gt;The unique common connections between node 452 and node 423 are 104, 832, 496, 906, 824, 470, 550, 766, 634, 740.&lt;/sub a&gt;<br>
        &lt;sub a&gt;10&lt;/sub a&gt;<br>
        &lt;final a&gt;Yes&lt;/final a&gt;
      </td>
    </tr>
  </table>
</div>



## Lost in distance for similarity tasks
When both distances are minimal, GPT4 and Llama-3-70B-Instruct exhibit the best performance. Llama-3-8B-Instruct, which has a high failure rate in following instructions as described in Appendix A.2, demonstrates the second-best performance, though it is not significantly different from the top performers. Specifically, performance at the largest distances is significantly worse compared to that at the smallest distances. As the distances increase (i.e., along the diagonal elements), the performance of all models deteriorates. In Llama-3-70B, we observe a 12% drop in model accuracy when the distance
between common connections for both |N (vi) ∩ N (vj )| and |N (vj ) ∩ N (vk)| increases, shifting from the (Small, Small) index to the (Large, Large) index in the heatmap plot. These results highlight that the lost-in-distance phenomenon adversely affects model performance in similarity tasks.

<img width="1048" alt="Screenshot 2025-01-26 at 11 23 56 AM" src="https://github.com/user-attachments/assets/aeae481a-18cd-42cb-b748-6957a9710fe6" />

## 4. Citation
```
@article{firooz2024lost,
  title={Lost-in-Distance: Impact of Contextual Proximity on LLM Performance in Graph Tasks},
  author={Firooz, Hamed and Sanjabi, Maziar and Jiang, Wenlong and Zhai, Xiaoling},
  journal={arXiv preprint arXiv:2410.01985},
  year={2024}
}
```

## 7. Contact
If you have any questions, please raise an issue or contact us at mhfirooz@gmail.com, wenlongwj@gmail.com.
