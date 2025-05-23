## Latex
1. [Cite range of papers](https://tex.stackexchange.com/questions/3871/citing-a-range-of-papers-using-numeric-keys-as-in-citea-b-c-1-3)
```
\documentclass{article}
\usepackage[style=numeric-comp]{biblatex}
\bibliography{xampl}
\begin{document}
hello \cite{article-full,book-full,mastersthesis-full}
\printbibliography
\end{document}
```
2. [Mathematical symbols](https://oeis.org/wiki/List_of_LaTeX_mathematical_symbols)

3. [Adjust width of algorithm](https://tex.stackexchange.com/questions/350434/adjust-width-of-algorithm-float)

4. [Add section without number to the table of content](https://tex.stackexchange.com/questions/30122/generate-table-of-contents-when-section-sections-without-numbering-has-been)
* If we donot want to keep the traditional numbered space
   ```
   \chapter{Glossary}

   \section*{List of Abbreviations}
   \addcontentsline{toc}{section}{List of Abbreviations}%

   \section*{List of Symbols}
   \addcontentsline{toc}{section}{List of Symbols}%
   ```
   ![fig](https://github.com/yuezhezhang/ROS_bug_list/blob/main/images/latex-4-1.png)
* If we want to keep the traditional numbered space
   ```
   \chapter{Glossary}

   \section*{List of Abbreviations}
   \addcontentsline{toc}{section}{\protect\numberline{}List of Abbreviations}%
   
   \section*{List of Symbols}
   \addcontentsline{toc}{section}{\protect\numberline{}List of Symbols}%
   ```
   ![fig](https://github.com/yuezhezhang/ROS_bug_list/blob/main/images/latex-4-2.png)
   
5. [Draw three-line table](https://zhuanlan.zhihu.com/p/440498868)
```
\begin{tabular}{cccccc}
   \toprule
   序号 & 姓名 & 性别 & 年龄 & 身高/cm & 体重/kg \\
   \midrule
   1 & 张三 & M & 16 & 163 & 50 \\
   2 & 王红 & F & 15 & 159 & 47 \\
   3 & 李二 & M & 17 & 165 & 52 \\
   \bottomrule
\end{tabular}
```
6. [Add an underbrace to a row vecor](https://tex.stackexchange.com/questions/519336/how-to-add-an-underbrace-to-the-part-of-the-row-vector)
```
\documentclass{article}
\usepackage{amsmath}

\begin{document}

\[
A = \begin{bmatrix}
    1&\smash{\underbrace{\begin{matrix}
        1&\dotsb&1
    \end{matrix}}_N}
\end{bmatrix}
\]

\end{document}
```
7. [Mathematical fonts](https://www.overleaf.com/learn/latex/Mathematical_fonts)

8. [Curly brace in equations](https://stackoverflow.com/questions/4027363/two-statements-next-to-curly-brace-in-an-equation)
```
\documentclass{article}
\usepackage{amsmath}

\begin{document}

\begin{equation}
  f(x)=\begin{cases}
    1, & \text{if $x<0$}.\\
    0, & \text{otherwise}.
  \end{cases}
\end{equation}

\end{document}
```
9. [multiple images in a row](https://stackoverflow.com/questions/52628649/multiple-subfigures-in-a-row-in-a-latex-document)
```
\usepackage{graphicx}
\usepackage{subfig}

\begin{figure}
 \centering
 \subfloat[]{\includegraphics[width=0.24\textwidth]{monalisa.jpg}} 
 \subfloat[]{\includegraphics[width=0.24\textwidth]{monalisa.jpg}} 
 \subfloat[]{\includegraphics[width=0.24\textwidth]{monalisa.jpg}}
 \subfloat[]{\includegraphics[width=0.24\textwidth]{monalisa.jpg}}
 \caption{(a) blah (b) blah (c) blah (d) blah}
 \label{fig:foobar}
\end{figure}
```
10. [adjust table size](https://tex.stackexchange.com/questions/10863/is-there-a-way-to-slightly-shrink-a-table-including-font-size-to-fit-within-th)
```
\usepackage{graphics}
\scalebox{0.9}{
\begin{tabular}
\end{tabular}
}
```
