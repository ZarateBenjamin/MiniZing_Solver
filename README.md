# MiniZing_Solver

%*******************************************************************************************************
% Numero de anuncios de cada tipo
var 0..15: x1;  % Anuncios en television  tarde
var 0..10: x2;  % Anuncios en television noche
var 0..25: x3;  % Anuncios en diarios
var 0..4: x4;   % Anuncios en revistas
var 0..30: x5;  % Anuncios en radio
%*******************************************************************************************************
% Maximizar la exposición
solve maximize 81*x1 + 93*x2 + 54*x3 + 75*x4 + 27*x5;
%*******************************************************************************************************
% Restricciones de cantidad máxima
constraint x1 <= 15;
constraint x2 <= 10;
constraint x3 <= 25;
constraint x4 <= 4;
constraint x5 <= 30;
%*******************************************************************************************************
% Restricciones presupuestarias
constraint x1 + x2 <= 20;
constraint 1920*x1 + 2931*x2 <= 50000;
constraint 192*x1 + 342*x2 <= 1800;
constraint 192*x1 + 342*x2 + 72*x3 + 114*x4 + 18*x5 <= 3000;
%*******************************************************************************************************
% Restricción de exclusividad (si se opta por modelo sin anuncios en TV noche cuando hay en diarios)
% Esta restricción se activa descomentando una de las dos siguientes líneas dependiendo del escenario:
%*******************************************************************************************************
% Para el uso de Diarios
 constraint x2 == 0;  % No hay anuncios en televisión durante la noche si hay en diarios
%*******************************************************************************************************
% Para el uso de Tv durante Noche
% constraint x3 == 0;  % No hay anuncios en diarios si hay en televisión durante la noche
%*******************************************************************************************************
% Salida de los resultados
output [
    "Anuncios en TV tarde: ", show(x1), "\n",
    "Anuncios en TV noche: ", show(x2), "\n",
    "Anuncios en diarios: ", show(x3), "\n",
    "Anuncios en revistas: ", show(x4), "\n",
    "Anuncios en radio: ", show(x5), "\n",
    "Calidad total de la exposición: ", show(81*x1 + 93*x2 + 54*x3 + 75*x4 + 27*x5)
];
%*******************************************************************************************************
