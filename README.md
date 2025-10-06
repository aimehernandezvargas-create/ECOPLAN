# SCRIPT DE PYTHON PARA ECOPLAN: MODELO PREDICTIVO DE HUELLA DE CARBONO

def predecir_huella_de_carbono(n_casas, n_paneles, n_arboles, n_fabricas, hay_sombra):
    """
    Simula un Modelo de Regresión Ponderada para predecir la Huella de Carbono.
    La IA aplica factores de optimización (sombra y ahorro pasivo) a los cálculos base.
    """
    # 1. Definición de Consumo y Generación Base (Valores de Simulación)
    CONSUMO_CASA_BASE = 100     # t CO2/año por casa
    CONSUMO_FABRICA = 500       # t CO2/año por fábrica
    GENERACION_PANEL_MAX = 50   # t CO2/año por panel (en condiciones ideales)
    AHORRO_ARBOL = 10           # t CO2/año de ahorro por enfriamiento pasivo
    
    # 2. Lógica de la IA: Factores de Predicción y Optimización
    
    # A. Predicción de Sombra (Ineficiencia)
    eficiencia_panel = 1.0 
    if hay_sombra:
        # La IA predice la ineficiencia: pérdida de 30% de eficiencia por mala ubicación
        eficiencia_panel = 0.7  
    
    # B. Optimización Pasiva (Ahorro)
    ahorro_pasivo_total = n_arboles * AHORRO_ARBOL
    
    # 3. CÁLCULO FINAL PREDICTIVO
    consumo_total_bruto = (n_casas * CONSUMO_CASA_BASE) + (n_fabricas * CONSUMO_FABRICA)
    generacion_neta = (n_paneles * GENERACION_PANEL_MAX * eficiencia_panel)
    
    huella_final = consumo_total_bruto - generacion_neta - ahorro_pasivo_total
    
    return max(0, huella_final) 

# --- Pruebas de Validación del Modelo ---
# Escenario Ineficiente: 3 casas, 2 paneles, 1 fábrica, con sombra
huella_mala = predecir_huella_de_carbono(n_casas=3, n_paneles=2, n_arboles=0, n_fabricas=1, hay_sombra=True)
# Escenario Optimizado: 3 casas, 2 paneles, 1 fábrica, SIN sombra, 2 árboles
huella_buena = predecir_huella_de_carbono(n_casas=3, n_paneles=2, n_arboles=2, n_fabricas=1, hay_sombra=False)
