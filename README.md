# CÓDIGO PARA A SOLUÇÃO DE UM MODELO DE UMA PLANTA
Esse documento tem o objetivo de expor as linhas de código de um modelo de uma planta feitas para para o resumo expandido "O USO DO SOFTWARE LIVRE GNU OCTAVE NA SOLUÇÃO DE PROBLEMAS DE CONTROLE ÓTIMO EM TEMPO DISCRETO" escrito para o 15º Congresso de Inovação, Ciência e Tecnologia – CONICT.

% A ideia deste programa e apresentar uma matriz que

% representa os valores assumidos por J e U

% Inicialmente vamos atribuir valores numericos para a e r

% O numero de periodos que f oi considerado e N = 2

a = 1/2;
r = 1/2;
N = 2;
M = N + 1;
% P rimeiramente vamos def inir uma matriz x, composta por zeros
% no f inal do algoritmo de P D esta matriz correspondera a matriz J
est = zeros(4, M ); % a matriz x e a matriz inicial
x = [0; a; 2 ∗ a; 3 ∗ a]; % est corresponde ao conjunto das variaveis de estado
u = [−2 ∗ a; −a; 0; a; 2 ∗ a]; % u corresponde ao conjunto de controle
est(1, :) = x;
% Agora iremos calcular os custos intermediarios e f inal
% Calculo do custo f inal
f or i = 1 : 4
g(i) = est(i)2;
end
J(:, M ) = g′;
% O calculo de J(:, M ) f ornece a ultima coluna da matriz x
% Calculo dos custos intermediarios
f or k = M − 1 : −1 : 1
f or i = 1 : 4
if i == 1 % primeiro estado
f or j = 1 : 3 % varia de 1 ate 3, pois so aceita tres sinais de controle nesse estado
Jx(i, j) = J(j, k + 1) + r ∗ u(j + 2)2; % calcula todos os custos
% O j + 2 acima representa as limita¸coes que o estado f ornece aos controles que sao aceitos,
devido as restricoes impostas pelo proprio problema que estamos resolvendo
end
[Y, I] = min(Jx(i, 1 : 3)); % escolhe o valor minimo e indica qual a posicao dele
J(i, k) = Y ; % representa o f uncional otimo para essa etapa
U (i, k) = (I − 1) ∗ a; % representa o controle otimo para essa etapa
% O ajuste em I − 1 e para achar qual sinal de controle f ornece o valor minimo
end
if i == 2 % segundo estado
f or j = 1 : 4 % varia de 1 ate 4, pois aceita quatro sinais de controle nesse estado
Jx(i, j) = J(j, k + 1) + r ∗ u(j + 1)2;
% O j + 1 representa as limita¸coes que o estado f ornece
% devido as restricoes impostas pelo proprio problema que estamos resolvendo
end
[Y, I] = min(Jx(i, 1 : 4));
J(i, k) = Y ;
M = N + 1;
U (i, k) = (I − 2) ∗ a;
% O ajuste de I − 2 e para achar qual sinal de controle f ornece o valor minimo
% O valor de U apresentado acima escolhe a melhor politica de controle
end
if i == 3 % terceiro estado
f or j = 1 : 4 % varia de 1 ate 4, pois aceita quatro sinais de controle nesse estado
Jx(i, j) = J(j, k + 1) + r ∗ u(j)2;
% O j e devido as limita¸coes do estado
end
[Y, I] = min(Jx(i, 1 : 4));
J(i, k) = Y ;
U (i, k) = (I − 3) ∗ a;
% O ajuste − 3 e para achar qual sinal de controle f ornece o valor minimo
end
if i == 4 % quarto estado
f or j = 1 : 3 % varia de 1 ate 3, pois so aceita tres sinais de controle nesse estado
Jx(i, j) = J(j + 1, k + 1) + r ∗ u(j)2;
% O j representa as limita¸coes do estado devido as restricoes impostas pelo problema
end
[Y, I] = min(Jx(i, 1 : 3));
J(i, k) = Y ;
U (i, k) = (I − 3) ∗ a;
% O ajuste de I − 3 e para achar qual sinal de controle f ornece o valor minimo
end
end
end
% Depois que o programa f oi executado, para encontrar as respostas para o f uncional,
% o estado e o controle basta digitar J (enter), x (enter) e U (enter)
