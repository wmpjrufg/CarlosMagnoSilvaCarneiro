<script src = "https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id = "MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

<h1>Comprimento de ancoragem necessário(\(l_{b,nec}\))</h1>

<p align="justify">
Para o cálculo do comprimento de ancoragem, é preciso obter a tensão de aderência de cálculo (\(f_{bd}\)), que depende de alguns fatores, tais como: (a) o tipo da barra, se é lisa ou nervurada (fator \(η_1\)), (b) a posição da barra na geometria da peça (fator \(η_2\)), (c) diâmetro da barra (fator \(η_3\)), além da (d) resistência de cálculo do concreto à tração (\(f_{ctd}\)). O cálculo é dado conforme equação (1):
</p> 

<table width = "100%" border = "0">
    <tr>
        <td width = "90%">
            <p>\[f_{bd}=η_1.η_3.η_3.f_{ctd}\]</p>
        </td>
        <td width = "10%">
            <p align="right">(1)</p>
        </td>
    </tr>
</table>

<ul>
    <li>\(\eta_1\) = 1,00 para barras lisas;</li>
    <li>\(\eta_1\) = 1,40 para barras entalhadas;</li>
    <li>\(\eta_1\) = 2,25 para barras nervuradas;</li>
    <li>\(\eta_2\) = 1,00 para situações de boa aderência;</li>
    <li>\(\eta_2\) = 0,70 para situações de má aderência;</li>
    <li>\(\eta_3\) = 1,00 para \(\phi_l < 32 mm\);</li>
    <li>\(\eta_3\) = \(\frac{132-\phi_l}{100}\) para \(\phi_l \geq 32 mm\).</li>
</ul>

<p align="justify">
A resistência do concreto à tração de cálculo (\(f_{ctd}\)) se dá através da equação (2): 
</p> 

<table width = "100%" border = "0">
    <tr>
        <td width = "90%">
            <p>\[f_{ctd}=\frac{f_{ctk,inf}}{\gamma_c}\]</p>
        </td>
        <td width = "10%">
            <p align="right">(2)</p>
        </td>
    </tr>
</table>

<p align="justify">
A partir disso, tem-se o comprimento básico de ancoragem (\(l_b\)), que tem que ser maior ou igual a 25.φ e conforme equação (3). A equação (4) apresenta o comprimento de ancoragem necessário (\(l_{b,nec}\))
</p> 

<table width = "100%" border = "0">
    <tr>
        <td width = "90%">
            <p>\[l_{b}=\frac{\phi}{4}.\frac{f_yd}{f_yd} \geq 25.\phi\]</p>
        </td>
        <td width = "10%">
            <p align="right">(3)</p>
        </td>
    </tr>
    <tr>
        <td width = "90%">
            <p>
                            \[l_{b,nec}=\alpha.l_{b}.\frac{A_{s,calc}}{A_{s,ef}}\geq \left\{\begin{matrix}0,30.l_b
                            \\10.\phi 
                            \\100 mm 
                            \end{matrix}\right.\]
            </p>
        </td>
        <td width = "10%">
            <p align="right">(4)</p>
        </td>
    </tr>
</table>

<ul>
    <li>\(\alpha\) = 0,70 sem gancho;</li>
    <li>\(\alpha\) = 1,00 com gancho;</li>
    <li>\(A_{s,calc}\) - Área de aço calculada;</li>
    <li>\(A_{s,ef}\) - Área de aço efetiva.</li>
</ul>

<p align="justify">
    <a href="https://wmpjrufg.github.io/2122ICPINASCIMENTO/ANCORAGEM/ANC.html" target="_blank">Acesso a ferramenta.</a>
</p> 