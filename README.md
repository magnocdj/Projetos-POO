package main;

import modelo.Apartamento;
import modelo.Casa;
import modelo.Financiamento;
import modelo.Terreno;
import util.InterfaceUsuario;

import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        // a. Todos os financiamentos deverão permanecer em um único ArrayList.
        List<Financiamento> financiamentos = new ArrayList<>();

        InterfaceUsuario interfaceUsuario = new InterfaceUsuario();

        // b. Pedir os dados do usuário para um financiamento.
        System.out.println("--- Entrada de Dados do 1º Financiamento (Casa) ---");
        double valorImovelUsuario = interfaceUsuario.pedirValorImovel();
        int prazoFinanciamentoUsuario = interfaceUsuario.pedirPrazoFinanciamento();
        double taxaJurosUsuario = interfaceUsuario.pedirTaxaFinanciamento();

        // Adiciona o primeiro financiamento (do tipo Casa) com os dados do usuário.
        financiamentos.add(new Casa(valorImovelUsuario, prazoFinanciamentoUsuario, taxaJurosUsuario));

        // c. Para os demais financiamentos, informar os dados diretamente no código.
        System.out.println("\nAdicionando financiamentos com dados pré-definidos...");

        // Adicionando 1 Casa, 2 Apartamentos e 1 Terreno
        financiamentos.add(new Casa(350000, 25, 0.085));
        financiamentos.add(new Apartamento(450000, 30, 0.09));
        financiamentos.add(new Apartamento(620000, 20, 0.08));
        financiamentos.add(new Terreno(150000, 10, 0.11));


        // d. Manter o texto que mostra a soma dos valores e a soma dos financiamentos.
        double totalValorImoveis = 0;
        double totalValorFinanciamentos = 0;
        int contador = 1;

        // Itera sobre a lista de financiamentos usando polimorfismo
        for (Financiamento f : financiamentos) {
            System.out.printf("\n--- Dados do Financiamento %d (%s) ---\n", contador, f.getClass().getSimpleName());
            System.out.printf("Valor do imóvel: R$ %.2f\n", f.getValorImovel());
            System.out.printf("Prazo: %d anos\n", f.getPrazoFinanciamento());
            System.out.printf("Taxa Anual: %.2f%%\n", f.getTaxaJurosAnual() * 100);
            System.out.printf("Valor da parcela mensal: R$ %.2f\n", f.calcularPagamentoMensal());
            System.out.printf("Valor total do financiamento: R$ %.2f\n", f.calcularTotalPagamento());

            totalValorImoveis += f.getValorImovel();
            totalValorFinanciamentos += f.calcularTotalPagamento();
            contador++;
        }

        // Exibe os totais
        System.out.println("\n-------------------------------------------");
        System.out.printf("Soma do valor de todos os imóveis: R$ %.2f\n", totalValorImoveis);
        System.out.printf("Soma do valor de todos os financiamentos: R$ %.2f\n", totalValorFinanciamentos);
        System.out.println("-------------------------------------------");
    }
