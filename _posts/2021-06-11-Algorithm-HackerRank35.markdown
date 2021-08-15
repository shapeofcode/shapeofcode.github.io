---
layout: post
title:  "HackerRank - Tree: Huffman Decoding"
date:   2021-06-11
last_modified_at: 2021-06-11
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Data Structures - Trees

<br/>

문제 설명 간략 :    

Huffman coding은 같은 문자의 빈번도가 높을 수 록 짧아지고 낮을 수 록 길어진다. 
모든 정점들은 코드가 포함되는데 노드의 왼쪽은 0 오른쪽은 1로 표시되고 노드에는 문자와 문자의 빈도가 포함된다.
루트 노드는 빈도수의 합으로 표현하고 왼쪽부터 높은 빈도를 표현한다.

0과 1로 표현된 encode된 string이 주어지고 decode된 문자열을 출력하라. 

<br/>

idea

s를 돌면서 char가 1이면 node의 오른쪽 0이면 node의 왼쪽으로 돌면서 node의 오른쪽 또는 왼쪽의 값이 null이면 
node의 data를 문자열에 붙이고 node를 다시 root로 돌려 탐색한다.

<br/>

제약사항

- 1 <= |s| <= 25

<br/>
   

<br/>

### 자바 풀이

```java
import java.util.*;

abstract class Node implements Comparable<Node> {
    public  int frequency; // the frequency of this tree
    public  char data;
    public  Node left, right;
    public Node(int freq) {
        frequency = freq;
    }

    // compares on the frequency
    public int compareTo(Node tree) {
        return frequency - tree.frequency;
    }
}

class HuffmanLeaf extends Node {


    public HuffmanLeaf(int freq, char val) {
        super(freq);
        data = val;
    }
}

class HuffmanNode extends Node {

    public HuffmanNode(Node l, Node r) {
        super(l.frequency + r.frequency);
        left = l;
        right = r;
    }

}


class Decoding {

/*  
	class Node
		public  int frequency; // the frequency of this tree
    	public  char data;
    	public  Node left, right;
    
*/

    void decode(String s, Node root) {

        StringBuilder sb = new StringBuilder();

        Node node = root;

        for(int i = 0 ; i < s.length(); i++) {
            node = s.charAt(i) == '1' ? node.right : node.left;
            if(node.left == null || node.right == null) {
                sb.append(node.data);
                node = root;
            }
        }

        System.out.println(sb);
    }



}


public class Solution {

    // input is an array of frequencies, indexed by character code
    public static Node buildTree(int[] charFreqs) {

        PriorityQueue<Node> trees = new PriorityQueue<Node>();
        // initially, we have a forest of leaves
        // one for each non-empty character
        for (int i = 0; i < charFreqs.length; i++)
            if (charFreqs[i] > 0)
                trees.offer(new HuffmanLeaf(charFreqs[i], (char)i));

        assert trees.size() > 0;

        // loop until there is only one tree left
        while (trees.size() > 1) {
            // two trees with least frequency
            Node a = trees.poll();
            Node b = trees.poll();

            // put into new node and re-insert into queue
            trees.offer(new HuffmanNode(a, b));
        }

        return trees.poll();
    }

    public static Map<Character,String> mapA=new HashMap<Character ,String>();

    public static void printCodes(Node tree, StringBuffer prefix) {

        assert tree != null;

        if (tree instanceof HuffmanLeaf) {
            HuffmanLeaf leaf = (HuffmanLeaf)tree;

            // print out character, frequency, and code for this leaf (which is just the prefix)
            //System.out.println(leaf.data + "\t" + leaf.frequency + "\t" + prefix);
            mapA.put(leaf.data,prefix.toString());

        } else if (tree instanceof HuffmanNode) {
            HuffmanNode node = (HuffmanNode)tree;

            // traverse left
            prefix.append('0');
            printCodes(node.left, prefix);
            prefix.deleteCharAt(prefix.length()-1);

            // traverse right
            prefix.append('1');
            printCodes(node.right, prefix);
            prefix.deleteCharAt(prefix.length()-1);
        }
    }

    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        String test= input.next();

        // we will assume that all our characters will have
        // code less than 256, for simplicity
        int[] charFreqs = new int[256];

        // read each character and record the frequencies
        for (char c : test.toCharArray())
            charFreqs[c]++;

        // build tree
        Node tree = buildTree(charFreqs);

        // print out results
        printCodes(tree, new StringBuffer());
        StringBuffer s = new StringBuffer();

        for(int i = 0; i < test.length(); i++) {
            char c = test.charAt(i);
            s.append(mapA.get(c));
        }

        //System.out.println(s);
        Decoding d = new Decoding();
        d.decode(s.toString(), tree);

    }
}


```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/tree-huffman-decoding/problem)