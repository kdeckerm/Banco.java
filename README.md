package sistemabancario;

// Clase Banco para probar los créditos
// Se encarga de crear diferentes tipos de créditos y mostrar sus cuotas calculadas
class SistemaBancario {

    public static void main(String[] args) {
        
        // Crear un cliente           // Nombre _ Cedula _ email _ Telefono _ Direccion   
        Cliente cliente1 = new Cliente("Juan Pérez", "12345678", "juan@email.com", "3001234567", "Calle 123"); 
        
        // Método principal (punto de entrada del programa)
        // Se encarga de ejecutar el programa e imprimir los cálculos de las cuotas
        CreditoPersonal cp = new CreditoPersonal(95000000, 5, 240); // Monto _ interes _ plazo
        System.out.println("Cuota Crédito Personal: " + cp.calcularCuota());
        
        CreditoEmpresarial ce = new CreditoEmpresarial(20000, 3000, 10);
        System.out.println("Cuota Crédito Empresarial: " + ce.calcularCuota());
        
        CreditoEspecial cs = new CreditoEspecial(15000, 15);
        System.out.println("Cuota Crédito Especial: " + cs.calcularCuota());
        
    }
    
}
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
package sistemabancario;

// Clase CreditoPersonal (hereda de Credito)
// Representa un crédito personal, donde la cuota mensual se calcula aplicando un porcentaje de interés
class CreditoPersonal extends Credito {
    
    private double interes; // Porcentaje de interés
    
    // Constructor de CreditoPersonal
    // Recibe el monto, el interés y el plazo del crédito personal
    public CreditoPersonal(double monto, double interes, int plazo) {
        super(monto, plazo); // Llamada al constructor de la superclase
        this.interes = interes;
    }
    
    // Implementación del método calcularCuota para Crédito Personal
    // Calcula la cuota mensual basada en el monto del crédito, el interés y el plazo
    // Retorna el valor de la cuota mensual
    @Override
    public double calcularCuota() {
        return (monto + (monto * (interes / 100))) / plazo; // Fórmula de cálculo de cuota
    }
    
}
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
package sistemabancario;

// Clase CreditoEspecial (sin interés, hereda de Credito)
// Representa un crédito especial en el que no se aplica ningún interés, la cuota se obtiene dividiendo el monto entre el plazo
class CreditoEspecial extends Credito{
    
    // Constructor de CreditoEspecial
    // Recibe el monto y el plazo del crédito especial
    public CreditoEspecial(double monto, int plazo) {
        super(monto, plazo); // Llamada al constructor de la superclase 
    }
    
    // Implementación del método calcularCuota para Crédito Especial
    // Calcula la cuota mensual dividiendo el monto total entre el plazo
    // No incluye intereses
    // Retorna el valor de la cuota mensual
    @Override
    public double calcularCuota() {
        return monto / plazo; // Fórmula de cálculo de cuota sin interés
    }
}
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
package sistemabancario;

// Clase CreditoEmpresarial (hereda de Credito)
// Representa un crédito empresarial, donde el interés es un valor fijo negociado en lugar de un porcentaje
class CreditoEmpresarial extends Credito{
    
    private double valorInteres; // Valor fijo de interés negociado  
    
    // Constructor de CreditoEmpresarial
    // Recibe el monto, el valor de interés fijo y el plazo
    public CreditoEmpresarial(double monto, double valorInteres, int plazo) {
        super(monto, plazo); // Llamada al constructor de la superclase
        this.valorInteres = valorInteres;
    }
    
    // Implementación del método calcularCuota para Crédito Empresarial
    // Calcula la cuota mensual sumando el monto con el interés fijo y dividiendo por el plazo
    // Retorna el valor de la cuota mensual
    @Override
    public double calcularCuota() {
        return (monto + valorInteres) / plazo; // Fórmula de cálculo de cuota
    }
    
}
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
package sistemabancario;

// Clase abstracta Credito
// Define una estructura base para los diferentes tipos de créditos
// Sirve como plantilla para los diferentes tipos de crédito y no puede ser instanciada directamente
abstract class Credito {
    
    protected double monto; // Monto del crédito
    protected int plazo; // Plazo en meses
    
    // Constructor de la clase Credito
    // Inicializa el monto y el plazo del crédito
    public Credito(double monto, int plazo) {
        this.monto = monto;
        this.plazo = plazo;
    }
    
    public abstract double calcularCuota();
    
}
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
package sistemabancario;

// Clase Cliente que almacena información del cliente del banco
// Representa un cliente del banco con información personal asociada
class Cliente {
    
    private String nombre;
    private String documento;
    private String correo;
    private String telefono;
    private String direccion;
    
    // Constructor de Cliente
    // Recibe los datos personales del cliente y los almacena en atributos
    public Cliente(String nombre, String documento, String correo, String telefono, String direccion) {
        this.nombre = nombre;
        this.documento = documento;
        this.correo = correo;
        this.telefono = telefono;
        this.direccion = direccion;
    }
    
    // Métodos getter para acceder a los atributos
    public String getNombre() { return nombre; }
    public String getDocumento() { return documento; }
    public String getCorreo() { return correo; }
    public String getTelefono() { return telefono; }
    public String getDireccion() { return direccion; }

    // Método para mostrar la información del cliente
    public void mostrarInfo() {
        System.out.println("Cliente: " + nombre + " - Documento: " + documento);
    }
}
/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
