<html lang = "pt-BR">
  	<head>
		<title>Concreto Armado-Ancoragem</title>
		<style>
			.entradas{
				width: 350px;
			}
			.entradas select{
				width: 100.00%;
			}
			.entradas input{
				width: 100.00%;
			}
		</style>
		<script src = "https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
		<script id = "MathJax-script" async src = "https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
  	</head>
  	<body>
		<h1><b>CALCULADORA CONCRETO ARMADO</b></h1>
			<h2><b>Comprimento de ancoragem</b></h2>
				<div class = 'entradas'>
				<h3>Entradas:</h3>
					<table>
						<tr>
							<td>Norma:</td>
							<td>
								<select id = "norma">
									<option value = "" data-default disabled selected></option>
									<option value = "NBR 6118">NBR 6118</option>
									<!--Estação de teste-->
									<!--
									<option value = "NBR 6118" selected>NBR 6118</option>
									-->
								</select>
							</td>
						</tr>
						<tr>
							<td>Tipo de barra:</td>
							<td>
								<select id = "tipo_1">
									<option value = "" data-default disabled selected></option>
									<option value = "LISA">Lisa</option>
									<option value = "ENTALHADA">Entalhada</option>
									<option value = "NERVURADA">Nervurada</option>
									<!--Estação de teste-->
									<!--
									<option value = "NERVURADA" selected>Lisa</option>
									-->
								</select>
							</td>
						</tr>
						<tr>
							<td>Tipo de aderência:</td>
							<td>
								<select id = "tipo_2">
									<option value = "" data-default disabled selected></option>
									<option value = "BOA">Boa</option>
									<option value = "MA">Má</option>
									<!--Estação de teste-->
									<!--
									<option value = "BOA" selected>Lisa</option>
									-->
								</select>
							</td>
						</tr>
						<tr>
							<td>\(f_{ck} (kPa)\):</td>
							<td><input type = "number" id = "f_ck" size = "40"> <br></td>
							<!--Estação de teste-->
							<!--
							<td><input type = "number" id = "f_ck" size = "40" value = 25000><br></td>
							-->
						</tr>
						<tr>
							<td>\(f_{yk} (kPa)\):</td>
							<td><input type = "number" id = "f_yk" size = "40"> <br></td>
							<!--Estação de teste-->
							<!--
							<td><input type = "number" id = "f_yk" size = "40" value = 500000><br></td>
							-->
						</tr>
						<tr>
							<td>\(\phi_l(m)\):</td>
							<td><input type = "number" id = "bitola" size = "40"> <br></td>
							<!--Estação de teste-->
							<!--
							<td><input type = "number" id = "bitola" size = "40" value = 0.016> <br></td>
							-->
						</tr>
						<tr>
							<td>\(A_{calc} (m²)\):</td>
							<td><input type = "number" id = "a_calc" size = "40"> <br></td>
							<!--Estação de teste-->
							<!--
							<td><input type = "number" id = "a_calc" size = "40" value = 1> <br></td>
							-->
						</tr>
						<tr>
							<td>\(A_{ef} (m²)\):</td>
							<td><input type = "number" id = "a_efet" size = "40"> <br></td>
							<!--Estação de teste-->
							<!--
							<td><input type = "number" id = "a_efet" size = "40" value = 1> <br></td>
							-->
						</tr>
						<tr>
							<td>Gancho?</td>
							<td>
								<select id = "gancho">
									<option value = "" data-default disabled selected></option>
									<option value = "SIM">Sim</option>
									<option value = "NÃO">Não</option>
									<!--Estação de teste-->
									<!--
									<option value = "SIM" selected>Sim</option>
									-->
								</select>
							</td>
						</tr>
					</table>
				</div>
					<br>
					<button id = 'calcular'>Calcular</button>
				<h3>Processamento:</h3>	
					<p>\(\eta_1\):</p>
					<p id = "n_1"></p>
					<p>\(\eta_2\):</p>
					<p id = "n_2"></p>	
					<p>\(\eta_3\):</p>
					<p id = "n_3"></p>
					<p>\(f_{ctm} (kPa)\):</p>
					<p id = "f_ctm"></p>
					<p>\(f_{ctinf} (kPa)\):</p>
					<p id = "f_ctinf"></p>
					<p>\(f_{ctd} (kPa)\):</p>
					<p id = "f_ctd"></p>
					<p>\(f_{bd} (kPa)\):</p>
					<p id = "f_bd"></p>
				<h3>Resultados:</h3>
					<p>\(l_{bas} (m)\):</p>
					<p id = "l_bas"></p>
					<p>\(l_{bmin} (m)\):</p>
					<p id = "l_bmin"></p>	
					<p>\(l_{b} (m)\):</p>
					<p id = "l_b"></p>
					<p>\(l_{necaux} (m)\):</p>
					<p id = "l_necaux"></p>
					<p>\(l_{necmin} (m)\):</p>
					<p id = "l_necmin"></p>
					<p>\(l_{bnec} (m)\):</p>
					<p id = "l_bnec"></p>
	<script>
		function ANCORAGEM() {	
			/*
			Esta função determina o comprimento de ancoragem de uma barra de aço em concreto.
			*/
			const NORMA = document.getElementById("norma").value;
			const ETA_1 = document.getElementById("tipo_1").value;
			const ETA_2 = document.getElementById("tipo_2").value;
			var F_CK = document.getElementById("f_ck").value;
			const F_YK = document.getElementById("f_yk").value;
			var BIT = document.getElementById("bitola").value;
			const AS_CALC = document.getElementById("a_calc").value;
			const AS_EF = document.getElementById("a_efet").value;
			const ALPHA_AUX = document.getElementById("gancho").value;

			// Cálculo do comprimento de ancoragem conforme item 9.3.2.1 da NBR 6118 (2014)
			if (NORMA == 'NBR 6118') {
				// Cálculo do fator η_1 
				if (ETA_1 == 'LISA') {
					N_1 = 1;
				} else if (ETA_1 == 'ENTALHADA') {
					N_1 = 1.40;
				} else if (ETA_1 == 'NERVURADA') {
					N_1 = 2.25;
				}
				//Cálculo do fator η_2
				if (ETA_2 == 'BOA') {
					N_2 = 1.00;
				} else if (ETA_2 == 'MA') {
					N_2 = 0.70;
				}
				//Cálculo do fator η_3
				BIT *= 1000;                 //Conversão m para mm
				if (BIT <= 32) {
					N_3 = 1.00;
				} else if (BIT > 32) {
					N_3 = (132 - BIT) / 100;
				}
				BIT /= 1000;                 //Conversão mm para m

				// Resistência de cálculo do concreto à tração direta (f_ctd)
				F_CK /= 1000;                // Conversão kPa para MPa 
				if (F_CK <= 50) {
					F_CTM = 0.3 * Math.pow(F_CK, (2 / 3));
				} else if (F_CK > 50) {
					F_CTM = 2.12 * Math.log(1 + 0.11 * F_CK);
				}
				F_CTM *= 1000;               // Conversão MPa para kPa 
				F_CTKINF = 0.70 * F_CTM;
				GAMMA_C = 1.40;
				F_CTD = F_CTKINF / GAMMA_C;
				F_CK *= 1000;                // Conversão MPa para kPa 
				
				// Resistência de aderência de cálculo(f_bd)
				F_BD = N_1 * N_2 * N_3 * F_CTD;
				
				// Comprimento de ancoragem básico (l_b)
				F_YD = F_YK / 1.15;
				L_BAUX = (BIT / 4) * (F_YD / F_BD);
				L_BMIN = 25 * BIT;
				L_B = Math.max(L_BAUX, L_BMIN);

				// Comprimento de ancoragem necessário (l_bnec)
				if (ALPHA_AUX == 'SIM') {
					ALPHA = 0.70;
				} else  if (ALPHA_AUX == 'NÃO') {
					ALPHA = 1.00;
				}
				L_BNECAUX = ALPHA * L_B *(AS_CALC / AS_EF);

				// Comprimento de ancoragem mínimo (l_cnecmin)
				L_BNECMIN1 = 0.3 * L_B;
				L_BNECMIN2 = 10 * BIT;
				L_BNECMIN3 = 0.10;
				L_BNECMIN = Math.max(L_BNECMIN1, L_BNECMIN2, L_BNECMIN3);

				// Comprimento de ancoragem utilizado (L_BNEC)
				L_BNEC = Math.max(L_BNECMIN, L_BNECAUX);
				
				// Processamento
				document.querySelector('#n_1').textContent = N_1;
				document.querySelector('#n_2').textContent = N_2;
				document.querySelector('#n_3').textContent = N_3;
				document.querySelector('#f_ctm').textContent = F_CTM;
				document.querySelector('#f_ctinf').textContent = F_CTKINF;
				document.querySelector('#f_ctd').textContent = F_CTD;
				document.querySelector('#f_bd').textContent = F_BD;
				
				// Resultado final
				document.querySelector('#l_bas').textContent = L_BAUX;
				document.querySelector('#l_bmin').textContent = L_BMIN;
				document.querySelector('#l_b').textContent = L_B;
				document.querySelector('#l_necaux').textContent = L_BNECAUX;
				document.querySelector('#l_necmin').textContent = L_BNECMIN;
				document.querySelector('#l_bnec').textContent = L_BNEC;
			}
		}

		// Função de chamada do clique do botão
		const PROCESSAR = document.getElementById("calcular");
		PROCESSAR.addEventListener('click', ANCORAGEM);
	</script>
  </body>
</html>