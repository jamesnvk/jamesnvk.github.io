---
layout: post
title: Mergesort
---

Mergesort in JavaScript was a fun algorithm to implement. It was the first algorithm that I coded that wasn't quadratic in run-time. It seems to me that solving problems with an O(n^2) run-time is easier on the brain, while solving problems in O(n log n) or less requires much more processing power. If only brains and computers could merge... *I'm looking at you Elon Musk*. You can check the full source code <a href="https://github.com/jamesnvk/algorithms-and-data-structures/blob/master/algorithms/mergesort.js" target="_blank">here</a>.

Mergesort is a staple divide and conquer algorithm. A divide and conquer algorithm is a design pattern that works by recursively breaking a problem down into smaller sub problems until the solutions to the sub problems can be combined to solve the bigger problem. Small problems are easier to solve than big problems, so we can take advantage of two partial solutions to construct a solution to the bigger overall problem. 

Mergesort does this in two (arguably) main steps - first breaking down the array into sub arrays until there is less than 2 elements (which makes it sorted since an array of 1 is automatically sorted), then implementing a merge routine. The main sorting happens during the merge routine, hence the name mergesort. The hardest part was implementing the merge routine. The trick is to keep track of the left and right arrays with pointers, incrementing the pointers as we move across the array in a loop while comparing elements. Once we reach the end of the array, concat the remaining elements in the opposing array and the array should be sorted.