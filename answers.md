  # CMPS 6610 Problem Set 02
## Answers

**Name:** <u>Rob Hartley</u>______



Place all written answers from `problemset-02.md` here for easier grading.

1. Prove that $\log n! \in \Theta(n \log n).$

     **Upper Bound**  

      Every factor in $n! \leq n$  
      $n! = (1 \cdot 2 \cdot 3 \ldots \cdot n)$  
      So:  
      $n! \leq n^n$  
      $\log n! \leq \log(n^n)$  
      $\log n! \leq n\log n$  
      $\log n! \in O(n \log n)$  

      **Lower Bound**  

      Suppose n is even, and we look at the greater half of the factorial, like this:  
      $\frac{n}{2} + 1, \frac{n}{2} + 2, \frac{n}{2} + 3, \ldots n$
      There would be $\frac{n}{2}$ of these factors, each of which is at least $\frac{n}{2}$  
      Therefore we know that $n! \geq {(\frac{n}{2})}^{n/2}$  
      So:  
      $\log n! \geq \log {(\frac{n}{2})}^{n/2}$  
      $\log n! \geq \frac{n}{2} \cdot \log (\frac{n}{2})$  
      $\log n! \geq (\frac{1}{2} \cdot n) \cdot \log (\frac{n}{2})$   
      $\log n! \geq (\frac{1}{2} \cdot n) \cdot (\log n - \log 2)$  
      $\log n! \geq (\frac{1}{2} \cdot n) \cdot (\log n) \cdot ( 1 - \frac{\log 2}{\log n})$  
      $\frac{\log 2}{\log n} \rightarrow 0$ as $n \rightarrow \infin$   
      $\log n! \geq (\frac{1}{2} \cdot n) \cdot (\log n) \cdot ( 1 - 0)$  
      $\log n! \geq (\frac{1}{2}) \cdot (n \cdot (\log n))$  
      and so $\log n! \in \Omega(n \log n)$  

      **Answer** 
      
      $
      \boxed{
      \begin{aligned}
      &\text{Since } \log n! \in O(n \log n)
      \text{ and } \log n! \in \Omega(n \log n) \\
      &\log n! \in \Theta(n \log n)
      \end{aligned}
      }
      $
     <br>  


2. (18 pts, 2pts ea.) **Recurrences**

  * $T(n)=2T(n/6)+1$  

    $T(\frac{n}{6}) = 2T(\frac{n}{36}) + 1$

    Level 1  
    $T(n) = 2 \cdot (2T(\frac{n}{36}) + 1) + 1$  
    $T(n) = 4T(\frac{n}{36}) + 3$  

    $T(\frac{n}{36}) = 2T(\frac{n}{216}) + 1$

    Level 2  
    $T(n) = 4 \cdot (2T(\frac{n}{216}) + 1) + 3$  
    $T(n) = 8T(\frac{n}{216}) + 7$  

    Generalized  
    $T(n) = 2^k T(\frac{n}{6^k}) + (2^k - 1)$

    Recursion Depth  
    $\frac{n}{6^k} = 1$  
    $n = 6^k$  
    $\log_6 n = k$  

    Substitute  
    $T(n) = 2^{\log_6 n} T(\frac{n}{6^{\log_6 n}}) + (2^{\log_6 n} - 1)$  
    $T(n) = n^{\log_6 2} T(1) + n^{\log_6 2} - 1$  

    $\boxed{T(n) \in O(n^{\log_6 2})}$  
    <br>



  * $T(n)=6T(n/4)+n$  

    $T(\frac{n}{4}) = 6T(\frac{n}{16}) + \frac{n}{4}$  

    Level 1  
    $T(n) = 6 \cdot (6T(\frac{n}{16}) + \frac{n}{4}) + n$  
    $T(n) = 36T(\frac{n}{16}) + n + \frac{6n}{4}$  

    $T(\frac{n}{16}) = 6T(\frac{n}{64}) + \frac{n}{16}$  

    Level 2  
    $T(n) = 36 \cdot (6T(\frac{n}{64}) + \frac{n}{16}) + n + \frac{6n}{4}$  
    $T(n) = 216T(\frac{n}{64}) + n + \frac{6n}{4} + \frac{36n}{16}$  

    Generalized Equation  
    $T(n) = 6^k T(\frac{n}{4^k}) + n \cdot \sum_{i=0}^{k-1}(\frac{6}{4})^i$  

    Geometric Series  
     $\alpha > 1$ so  $ \sum_{i=0}^n \alpha^i  \leq \frac{\alpha}{\alpha - 1}\cdot\alpha^n$  
    $\sum_{i=0}^{k-1}(\frac{6}{4})^i \leq (\frac{\frac{6}{4}}{\frac{6}{4} - 1}) \cdot (\frac{6}{4})^{k - 1}$  
    $\sum_{i=0}^{k-1}(\frac{6}{4})^i \leq 3 \cdot (\frac{6}{4})^{k - 1}$  

    Recursion Depth  
    $\frac{n}{4^k} = 1$  
    $n = 4^k$  
    $k = \log_4 n$  

    Substitute into Generalized Equation  
    $T(n) \leq 6^k T(\frac{n}{4^k}) + 3n \cdot (\frac{6}{4})^{k - 1}$  
    $T(n) \leq 6^{\log_4 n} T(\frac{n}{4^{\log_4 n}}) + 3n \cdot (\frac{6}{4})^{\log_4 n - 1}$  
    $T(n) \leq n^{\log_4 6} T(1) + 3n \cdot \frac{(\frac{6}{4})^{\log_4 n}}{\frac{6}{4}}$  
    $T(n) \leq n^{\log_4 6} T(1) + 2n \cdot n^{\log_4 \frac{6}{4}}$  
    $T(n) \leq n^{\log_4 6} T(1) + 2n^{(1 +\log_4 \frac{6}{4})}$  
    $T(n) \leq n^{\log_4 6} T(1) + 2n^{(\log_4 4 +\log_4 \frac{6}{4})}$  
    $T(n) \leq n^{\log_4 6} T(1) + 2n^{(\log_4 (4 \cdot \frac{6}{4}))}$  
    $T(n) \leq n^{\log_4 6} T(1) + 2n^{\log_4 6}$  
    $T(n) \leq (n^{\log_4 6}) \cdot (c + 2)$

    $\boxed{T(n) \in O(n^{\log_4 6})}$  
    <br>

  * $T(n)=7T(n/7)+n$  
  Brick Method  
  $T(n)=aT\left(\frac{n}{b}\right)+n^d$  
  $a = 7, b =7, d = 1$  
  $a = b^d$ ~ $ balanced: \ \  \Theta(n^d\log n)$  
    
     $\boxed{T(n) \in O(n\log n)}$  
    <br>

  * $T(n)=9T(n/4)+n^2$  
  Brick Method  
  $T(n)=aT\left(\frac{n}{b}\right)+n^d$  
  $a = 9, b = 4, d = 2$  
  $a < b^d$ ~ $ root \  dominated: \ \  \Theta(n^d)$ 

    $\boxed{T(n) \in O(n^2)}$  
  <br>

  * $T(n)=4T(n/2)+n^3$  

    $T(\frac{n}{2}) = 4T(\frac{n}{4}) + (\frac{n}{2})^3$  
    
    Level 1  
    $T(n) = 4 \cdot (4T(\frac{n}{4}) +  (\frac{n}{2})^3) + n^3$  
    $T(n) = 16T(\frac{n}{4}) +  4 \cdot (\frac{n}{2})^3 + n^3$  

    $T(\frac{n}{4}) = 4T(\frac{n}{8}) + (\frac{n}{4})^3$  

    Level 2  
    $T(n) = 16 \cdot (4T(\frac{n}{8}) + (\frac{n}{4})^3) +  4 \cdot (\frac{n}{2})^3 + n^3$  
    $T(n) = 64T(\frac{n}{8}) + 16 \cdot (\frac{n}{4})^3 +  4 \cdot (\frac{n}{2})^3 + n^3$  

    $T(n) = 64T(\frac{n}{8}) + \frac{1}{4}n^3 +  \frac{1}{2}n^3 + n^3$  

    Generalized Equation  
    $T(n) = 4^kT(\frac{n}{2^k}) + n^3 \cdot \sum_{i=0}^{k-1}(\frac{1}{2})^i$  

    Geometric Series  
    $\alpha < 1$ so $\sum_{i=0}^{\infin} \alpha^i  = \frac{1}{1 -\alpha}$  
    $\sum_{i=0}^{k-1}(\frac{1}{2})^i < \frac{1}{1 - \frac{1}{2}}$  
    $\sum_{i=0}^{k-1}(\frac{1}{2})^i < 2$  

    Recursion Depth  
    $\frac{n}{2^k} = 1$  
    $n = 2^k$  
    $k = \lg n$  

    Substitute into Generalized Equation  
    $T(n) \leq 4^kT(\frac{n}{2^k}) + n^3 \cdot 2$  
    $T(n) \leq 4^{\lg n}T(\frac{n}{2^{\lg n}}) + 2n^3$  
    $T(n) \leq n^{\lg 4}T(1) + 2n^3$  
    $T(n) \leq cn^2 + 2n^3$  

    $\boxed{T(n) \in O(n^3)}$  
    <br>  

  * $T(n)=49T(n/25)+n^{3/2}\log n$  

    $T(\frac{n}{25}) = 49T(\frac{n}{25^2}) + (\frac{n}{25})^{3/2}\log (\frac{n}{25})$  

    Level 1  
    $T(n) = 49 \cdot (49T(\frac{n}{25^2}) + (\frac{n}{25})^{3/2}\log (\frac{n}{25})) + n^{3/2}\log n$  
    $T(n) = 49^2T(\frac{n}{25^2}) + 49(\frac{n}{25})^{3/2}\log (\frac{n}{25}) + n^{3/2}\log n$  

    $T(\frac{n}{25^2}) = 49T(\frac{n}{25^3}) + (\frac{n}{25^2})^{3/2}\log (\frac{n}{25^2})$  

    Level 2  
    $T(n) = 49^2 \cdot (49T(\frac{n}{25^3}) + (\frac{n}{25^2})^{3/2}\log (\frac{n}{25^2})) + 49(\frac{n}{25})^{3/2}\log (\frac{n}{25}) + n^{3/2}\log n$  
    $T(n) = 49^3T(\frac{n}{25^3}) + 49^2(\frac{n}{25^2})^{3/2}\log (\frac{n}{25^2}) + 49(\frac{n}{25})^{3/2}\log (\frac{n}{25}) + n^{3/2}\log n$  

    Generalized Equation  
    $T(n) = 49^kT(\frac{n}{25^k}) + \sum_{i = 0}^{k -1}49^i(\frac{n}{25^i})^{3/2}\log(\frac{n}{25^i})$  

    Recursion Depth  
    $\frac{n}{25^k} = 1$  
    $n = 25^k$  
    $k = \log_{25}n$  

    Substitute into Generalized Equation  
    $T(n) = 49^{\log_{25}n}T(\frac{n}{25^{\log_{25}n}}) + \sum_{i = 0}^{{\log_{25}n} -1}49^i(\frac{n}{25^i})^{3/2}\log(\frac{n}{25^i})$  
    $T(n) = n^{\log_{25}49}T(1) + \sum_{i = 0}^{{\log_{25}n} -1}49^i(\frac{n^{3/2}}{25^{\frac{3i}{2}}})\log(\frac{n}{25^i})$  
    $T(n) = n^{\log_{25}49}T(1) + n^{3/2} \cdot \sum_{i = 0}^{{\log_{25}n} -1}(\frac{49}{\sqrt{25}^3})^i\log(\frac{n}{25^i})$ 

    Geometric Series  
    $\alpha < 1$ so $\sum_{i=0}^{\infin} \alpha^i  = \frac{1}{1 -\alpha}$  
    $\log\frac{n}{25^i} \leq \log n$  
    $\sum_{i = 0}^{{\log_{25}n} -1}(\frac{49}{\sqrt{25}^3})^i \cdot \log n$  
    $\log n \cdot\sum_{i = 0}^{{\log_{25}n} -1}(\frac{49}{125})^i$  
    $\sum_{i=0}^{\infin} (\frac{49}{125})^i = \frac{1}{1 - \frac{49}{125}} = \frac{125}{76} = c$  
    $\log n \cdot c$

    Substitute into Generalized Equation 2  
    $T(n) \leq n^{\log_{25}49} \cdot T(1) + n^{3/2} \cdot \log n \cdot \frac{125}{76}$  
    $T(n) \in O(n^{\log_{25}49} + n^{3/2} \cdot \log n)$  
    $\log_{25}49 \approx 1.21 < 3/2$  

    $\boxed{T(n) \in O(n^{3/2}\log n)}$  
    <br>


  * $T(n)=T(n-1)+2$  

    $T(n - 1) = T(n-2) + 2$  

    Level 1  
    $T(n) = (T(n-2) + 2) + 2$  
    $T(n) = T(n-2) + 4$  

    $T(n - 2) = T(n - 3) + 2$  

    Level 2  
    $T(n) = (T(n-3) + 2) + 4$  
    $T(n) = T(n-3) + 6$  

    Generalized Equation  
    $T(n) = T(n - k) + 2k$

    Recursion Depth  
    $n - k = 1$  
    $k = n - 1$  

    Substitute into Generalized Equation  
    $T(n) = T(n - (n - 1)) + 2(n-1)$  
    $T(n) = $T(1) + 2n - 2$  

    $\boxed{T(n) \in O(n)}$  
    <br>  
  * $T(n)= T(n-1)+n^c$, with $c\geq 1$  

    $T(n - 1) = T((n- 1) -1) + (n - 1)^c$  
    
    Level 1  
    $T(n) = T((n- 1) -1) + (n - 1)^c + n^c$  
    $T(n) = T(n -2) + (n - 1)^c + n^c$  

    $T(n - 2) = T((n- 2) -1) + (n - 2)^c$  

    Level 2  
    $T(n) = T((n- 2) -1) + (n - 2)^c + (n - 1)^c + n^c$  
    $T(n) = T(n -3) + (n - 2)^c + (n - 1)^c + n^c$  

    Generalized Equation  
    $T(n) = T(n - k) + \sum_{i = 0}^{k - 1}(n - i)^c$  

    Recursion Depth  
    $n - k = 1$  
    $k = n - 1$  

    Power Sum  
    $\sum_{i = 0}^{n}(n - i)^c$ is in the format of:  
    $\sum_{i = 1}^{n}i^c$  
    $\sum_{i = 1}^{n}i^c = \sum_{i = 1}^n \in \Theta(n^{c + 1})$

    Substitute into Generalized Equation  
    $T(n) = T(n - (n - 1)) + \sum_{i = 0}^{(n-1) -1}(n - i)^c$  
    $T(n) = T(1) + \Theta(n^{c + 1})$  

    $\boxed{T(n) \in O(n^{c + 1})}$
<br>

  * $T(n)=T(\sqrt{n})+1$  

    $T(n^{\frac{1}{2}}) = T((n^{\frac{1}{2}})^{\frac{1}{2}}) + 1$  
    Level 1  
    $T(n) = [T((n^{\frac{1}{2}})^{\frac{1}{2}}) + 1] + 1$  
    $T(n) = T(n^{\frac{1}{4}}) + 1 + 1$  

    $T(n^{\frac{1}{4}}) = T((n^{\frac{1}{4}})^{\frac{1}{2}}) + 1$  

    Level 2  
    $T(n) = [T((n^{\frac{1}{4}})^{\frac{1}{2}}) + 1] + 1 + 1$  
    $T(n) = T(n^{\frac{1}{8}}) + 1 + 1 + 1$  

    Generalized Equation  
    $T(n) = T(n^{\frac{1}{2^k}}) + \sum_{i = 0}^{k - 1} 1$  
    $T(n) = T(n^{\frac{1}{2^k}}) + k$

    Recursion Depth  
    $n^{\frac{1}{2^k}} \leq 2$  
    $\lg (n^{\frac{1}{2^k}}) \leq \lg (2)$  
    $\frac{1}{2^k} \cdot \lg n \leq 1$  
    $\lg n \leq 2^k$  
    $\lg \lg n \leq k$

    Substitute into Generalized Equation  
    $T(n) = T(n^{\frac{1}{2^{\lg \lg n}}}) + \lg \lg n$  
    $T(n) = T(n^{\frac{1}{\lg n}}) + \lg \lg n$  
    $n = 2^{\lg n}$  
    $T(n) = T({(2^{\\lg n}})^{\frac{1}{\lg n}}) + \lg \lg n$  
    $T(n) = T(2) + \lg \lg n$  

    $\boxed{T(n) \in O(\lg \lg n)}$
    <br>

3. (8 pts) **Algorithm Selection**

4. (8 pts) **More Algorithm Selection** 
 
5. (4 pts) **Integer Multiplication Timing Results**
