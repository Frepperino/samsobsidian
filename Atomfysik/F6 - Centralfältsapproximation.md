**Vad är centralfältsapproximation?**
Den fullständiga Hamiltonoperatorn för en N-elektron atom kan ej lösas i Schrödingerekvationen p.g.a. termen för elektron-elektron-repulsion. Därmed gör vi en **centralfältsapproximation** som förenklar $V(r,\theta,\phi)\approx V(r)$. Alltså pekar kraften utåt, parallellt mer $r$.  Vi approximerar då kärnan och resten av elektronerna till en punktladdning/laddningsmoln i centrum.

**Screening**
I denna metod använder vi **screening** som den negativa punktladdning/laddningsmoln av elektronerna som skärmar elektronen från den positiva kärnans punktladdning/laddningsmoln.

Vi får då ekvationen:
$$\hat{H}=\sum_{i=1}^{N}\left(-\frac{\hbar^2}{2m}\nabla_i^2 + V_{central}(r_i)\right) + V_{residual}$$
Där $|\sum_{i=1}^NV_{central}(r_i)| \gg |V_{residual}|$. Vi får
$$\hat{H}_{central}=\sum_{i=1}^{N}\left(-\frac{\hbar^2}{2m}\nabla_i^2 + V_{central}(r_i)\right)$$
$$\hat{H}_{central}=\sum_{i=1}^N\hat{H}_i$$
$$\hat{H}_i=-\frac{\hbar^2}{2m}\nabla^2_i+V_{central}(r_i)$$
$$\hat{H}_i\psi_i(r_i)=E_i\psi_i(r_i)$$
$$\psi(r_1,...,r_N)=\psi_1(r_1)...\psi_N(r_N)$$
$$E=E_1 + E_2 + ... + E_N$$
Precis som innan blir varje lösning på formen,
$$\psi_i(r_i)=R_i(r_i)Y_i(\theta_i,\phi_i)$$
med analoga kvanttal till vätefallet fast med subfix i.

Centralfältsapproximation ger oss skalmodellen med kvanttalen $l, m_l,n,m_s$.

**Skalmodellen**
Egenskaper för energitillstånden i skalmodellen:
- Energin bestäms av kvanttalen $n,l$ (förutom i väte). Energin ökar med $n$ och $l$ där ökat $n$ leder till stora hopp och ökande $l$ leder till mindre hopp för ett givet $n$.
- Utan ett magnetfält degenereras $m_l,m_s$. Det finns $2(2l + 1)$ degenererade tillstånd. De degenererade tillstånden med samma $n$ **och** $l$ skapar ett **skal**. D.v.s. 2s, 2p, 4d är alla olika skall.

Elektroner är ej utskiljbara, fermioner.

Större $n$ betyder inte nödvändigtvis att energin är högre. Beror även på $l$ (förutom i väte).

Med degenerationssambandet ser vi at $l = 0 \rightarrow 2$ , $l=1 \rightarrow 6$, $l=2 \rightarrow 10$. Systemet för att visa elektronkonfiguration:
![[Pasted image 20231205112240.png]]
Ex. Na = $1s^22s^22p^63s^1$. Alt. \[Ne]$3s^1$.

![[Pasted image 20231205112547.png|500]]
Finns några undantag, men inget vi behöver kunna nog.

