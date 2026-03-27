# Mi-repositorio

# Proyecto Lasañas en Java

## Descripción

Este proyecto consiste en una aplicación desarrollada en Java que calcula el precio de diferentes tipos de lasañas según su sabor, tamaño y extras.

## Cómo ejecutar

1. Abrir el proyecto en NetBeans o cualquier IDE compatible con Java.
2. Ejecutar la clase principal (Main o RestauranteMisPastas).
3. Ver los resultados en la consola.

## Autor

Juan Sebastián Rodríguez

Codigo adjunto:

/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 */

package com.mycompany.restaurantemispastas;

/**
 *
 * @author juans
 */
public class Restaurantemispastas {

    public static void main(String[] args) {

        Lasanas[] Lasanas1 = new Lasanas[5];
        Lasanas1[0] = new Lasanas("carne", "4_porciones", 22000.0);
        Lasanas1[1] = new ExtraQueso("pollo", "12_porciones", 25000.0, "provolone");
        Lasanas1[2] = new ExtraVegetales("camarones", "12_porciones", 18000.0, "champiñones");
        Lasanas1[3] = new ExtraVegetales("espinaca", "4_porciones", 25000.0, "calabacitas");
        Lasanas1[4] = new Lasanas();
        ValorTotal respuesta1 = new ValorTotal(Lasanas1);
        respuesta1.mostrarTotales();
        System.out.println();

        Lasanas[] Lasanas2 = new Lasanas[4];
        Lasanas2[0] = new Lasanas();
        Lasanas2[1] = new Lasanas("pollo", "12_porciones", 23000.0);
        Lasanas2[2] = new ExtraQueso("espinaca", "4_porciones", 25000.0, "suizo");
        Lasanas2[3] = new ExtraVegetales("carne", "12_porciones", 23000.0, "calabacitas");
        ValorTotal respuesta2 = new ValorTotal(Lasanas2);
        respuesta2.mostrarTotales();
        System.out.println();
    }
}

class Lasanas {
    private final static Double PRECIOBASE = 20000.0;
    private final static String SABOR = "pollo";
    private final static String TAMANO = "1_porcion";

    private String sabor;
    private String tamano;
    private Double precioBase;

    public Lasanas(String sabor, String tamano, Double precioBase) {
        this.sabor = sabor;
        this.tamano = tamano;
        this.precioBase = precioBase;
    }

    public Lasanas() {
        this.sabor = SABOR;
        this.tamano = TAMANO;
        this.precioBase = PRECIOBASE;
    }

    public String getSabor()      { return sabor; }
    public String getTamano()     { return tamano; }
    public Double getPrecioBase() { return precioBase; }

    public double calcularPrecio() {
        double precio = precioBase;

        if (sabor.equals("espinaca"))           { precio += precioBase * 0.10; }
        else if (sabor.equals("pollo"))         { precio += precioBase * 0.20; }
        else if (sabor.equals("carne"))         { precio += precioBase * 0.30; }
        else if (sabor.equals("camarones"))     { precio += precioBase * 0.40; }

        if (tamano.equals("1_porcion"))         { precio += 2000; }
        else if (tamano.equals("4_porciones"))  { precio += 6000; }
        else if (tamano.equals("12_porciones")) { precio += 15000; }

        return precio;
    }
} 

class ExtraQueso extends Lasanas {
    private String tipoQueso;

    public ExtraQueso(String sabor, String tamano, Double precioBase, String tipoQueso) {
        super(sabor, tamano, precioBase);
        this.tipoQueso = tipoQueso;
    }

    @Override
    public double calcularPrecio() {
        double precio = super.calcularPrecio();
        if (tipoQueso.equals("provolone"))      { precio += 5000; }
        else if (tipoQueso.equals("suizo"))     { precio += 6000; }
        return precio;
    }
}   

class ExtraVegetales extends Lasanas {
    private String tipoVegetales;

    public ExtraVegetales(String sabor, String tamano, Double precioBase, String tipoVegetales) {
        super(sabor, tamano, precioBase);
        this.tipoVegetales = tipoVegetales;
    }

    @Override
    public double calcularPrecio() {
        double precio = super.calcularPrecio();
        if (tipoVegetales.equals("champiñones"))      { precio += 4000; }
        else if (tipoVegetales.equals("calabacitas")) { precio += 3000; }
        return precio;
    }
}   

class ValorTotal {
    private Double valorTotalLasanas = 0.00;
    private Double valorTotalExtraQueso = 0.00;
    private Double valorTotalExtraVegetales = 0.00;
    private Lasanas[] lasanas;

    public ValorTotal(Lasanas[] lasanas) {
        this.lasanas = lasanas;
    }

    public void mostrarTotales() {
        double totalLasanas = 0;

        for (Lasanas l : lasanas) {
            double precio = l.calcularPrecio();
            if (l instanceof ExtraQueso)          { valorTotalExtraQueso += precio; }
            else if (l instanceof ExtraVegetales) { valorTotalExtraVegetales += precio; }
            else                                  { valorTotalLasanas += precio; }

           totalLasanas+=precio;
        }
        System.out.println(Math.round(valorTotalLasanas));
        System.out.println(Math.round(valorTotalExtraQueso));
        System.out.println(Math.round(valorTotalExtraVegetales));
        System.out.println(Math.round(totalLasanas));
  
    }
}   
    
