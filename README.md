# CÓDIGO PARA A SOLUÇÃO DE UM MODELO DE UMA PLANTA
Esse documento tem o objetivo de expor as linhas de código de um modelo de uma planta feitas para para o resumo expandido "O USO DO SOFTWARE LIVRE GNU OCTAVE NA SOLUÇÃO DE PROBLEMAS DE CONTROLE ÓTIMO EM TEMPO DISCRETO" escrito para o 15º Congresso de Inovação, Ciência e Tecnologia – CONICT.

% Variáveis do problema

a=0.5;

r=0.5;

N=2;

M=N+1;

% Variáveis iniciais

x=zeros(4,M);

x(:,1)=[0; a; 2*a; 3*a];

u=[-2*a; -a; 0; a; 2*a];

% Custo final

for i=1:4

    g(i)=x(i)^2;

end

J(:,M)=g';

% Custos ótimos intermediários

for k=M-1:-1:1

    for i=1:4
    
        if i==1
        
            for j=1:3
            
                Jx(i,j)=J(j,k+1)+r*u(j+2)^2;
            
            end
            
            [Y,I]=min(Jx(i,1:3));
            
            J(i,k)=Y;
            
            U(i,k)=(I-1)*a;
       
        end
        
        if i==2
        
            for j=1:4
            
                Jx(i,j)=J(j,k+1)+r*u(j+1)^2;
            
            end
            
            [Y,I]=min(Jx(i,:));
            
            J(i,k)=Y;
            
            U(i,k)=(I-2)*a;
        
        end
        
        if i==3
        
            for j=1:4
            
                Jx(i,j)=J(j,k+1)+r*u(j)^2;
            
            end
            
            [Y,I]=min(Jx(i,:));
            
            J(i,k)=Y;
            
            U(i,k)=(I-3)*a;
        
        end
        
        if i==4
        
            for j=1:3
            
                Jx(i,j)=J(j+1,k+1)+r*u(j)^2;
            
            end
            
            [Y,I]=min(Jx(i,1:3));
            
            J(i,k)=Y;
            
            U(i,k)=(I-3)*a;
        
        end
    
    end


end


% Sinal de controle e trajetória ótimos

for i=1:4

    L=i;
    
    for k=1:N
    
        us(i,k)=U(L,k);
        
        x(i,k+1)=x(i,k)+us(i,k);
        
        if x(i,k+1)==x(1,1)
        
            L=1;
        
        end
        
        if x(i,k+1)==x(2,1)
        
            L=2;
        
        end
        
        if x(i,k+1)==x(3,1)
        
            L=3;
        
        end
        
        if x(i,k+1)==x(4,1)
        
            L=4;
        
        end
    
    end

end

k=0:N;

figure

hold on

stairs(k,x(1,:))

stem(k(2:N+1),us(1,:),'r')

axis([0 N+1 -abs(3*a) abs(3*a)])

title('Estado e controle ótimo, x(0)=0')

legend('Estado','Controle ótimo')

xlabel('Período')

grid

figure

hold on

stairs(k,x(2,:))

stem(k(2:N+1),us(2,:),'r')

axis([0 N+1 -abs(3*a) abs(3*a)])

title('Estado e controle ótimo, x(0)=a')

legend('Estado','Controle ótimo')

xlabel('Período')

grid

figure

hold on

stairs(k,x(3,:))

stem(k(2:N+1),us(3,:),'r')

axis([0 N+1 -abs(3*a) abs(3*a)])

title('Estado e controle ótimo, x(0)=2*a')

legend('Estado','Controle ótimo')

xlabel('Período')

grid

figure

hold on

stairs(k,x(4,:))

stem(k(2:N+1),us(4,:),'r')

axis([0 N+1 -abs(3*a) abs(3*a)])

title('Estado e controle ótimo, x(0)=3*a')

legend('Estado','Controle ótimo')

xlabel('Período')

grid


% Depois que o programa foi executado, para encontrar as respostas para o funcional,

% o estado e o controle basta digitar J (enter), x (enter) e U (enter)
