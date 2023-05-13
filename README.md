# Proyecto: Aplicación que permita cargar un archivo de tipo .json, Editarlo y eliminarlo


# Alumno: Herrera Pacheco Gerardo Isidro ISC 4B 68612

## Se crea el JFrame con los elementos.

Se le añaden: 
1) TxtArea donde se mostrará el contenido del archivo seleccionado y tambien se podra editar el archivo ahi mismo.
2) Boton Archivo. Para buscar y seleccionar el archivo
3) Botón guardar. Para guardar los cambios hechos en el archivo
4) Botón eliminar. Para eliminar el archivo
5) ComboBox. Para poder seleccionar el tipo de archivo a buscar (Esto yo se le lo agregue adicionalmente).
Y le di formato a los elementos.

[![Captura-interfaz.png](https://i.postimg.cc/nLfZ92fG/Captura-interfaz.png)](https://postimg.cc/DS6RtqZS)

## Dar funcionalidad al botón archivo al hacer clic.

Se crea un JFileChooser para cuando se le de clic al botón se abra un panel para elegir el archivo. Se hace un "filtro" con el FileNameExtensionFilter para elegir que tipo de archivo abrir, esto lo toma del comboBox donde se podrá elegir txt o json. Luego se muestra este cuadro. Se hace el if para si se seleecionó cancelar no haga, si se dio aceptar lo siguiente es que el textField se muestra la ruta y luego con un while se inserta caracter por carácter en un string para que al final se inserte en el textArea. Todo esto dentro de un tryCatch para evitar errores de ejecución.

```
private void btnArchivoMouseClicked(java.awt.event.MouseEvent evt) {                                        
    System.out.println("Inico de la carga de archivo");
    JFileChooser fc = new JFileChooser();
    FileNameExtensionFilter filter = new FileNameExtensionFilter("Archivos de texto o       json",cmboxTipoArchivo.getSelectedItem().toString());

    fc. setFileFilter(filter);
    int seleccion = fc. showOpenDialog(this);
    if(seleccion == JFileChooser.CANCEL_OPTION){

    }else if(seleccion == JFileChooser.APPROVE_OPTION){
        File archivoSeleccionado = fc.getSelectedFile();
        this.txtArchivo.setText( archivoSeleccionado.getAbsolutePath());

        try( FileReader fr = new FileReader(archivoSeleccionado)){
            String cadena = "";
            int valor = fr.read();
            while (valor != -1){
                cadena += (char) valor;
                valor = fr.read();
            }
            this.txtAreaEntrada.setText(cadena);
        } catch(IOException e){
    e.printStackTrace();
        }
    }

} 

```

## Dar funcionalidad al botón guardar al hacer click.

Primero le agregué un if para comprobar si el textField esta vacio, si esto es asi no se ha importado ningún archivo y entonces cuando se oprime botón guardar sale un cuadro de dialogo. De ya haber mostrado un archivo, los cambios que se haga en el txtArea se guardarán. Para esto se crea un archivo file y se usa el PrintWriter, para poder escribir dentro de el con ayuda del método print() tomando como argumento el contenido del txtArea. Por ultimo se cierra para evitar cambios con el close(). Todo esto dentro de un Try Catch para atrapar cualquier excepción de tipo FileNotFoundException y mostrarlo en la consola con una descripción.

```
private void btnGuardarMouseClicked(java.awt.event.MouseEvent evt) {                                        
    if(txtArchivo.getText().isEmpty()){
        JOptionPane.showMessageDialog(null, "Seleccione un archivo del tipo requerido");
    }else {
        System.out.println("Inico guardar archivo");
        File archivo = new File(this.txtArchivo.getText());
        PrintWriter escribir;
        try {
            escribir = new PrintWriter(archivo);
            escribir.print(txtAreaEntrada.getText());
            escribir.close();
        } catch (FileNotFoundException ex) {
        // Logger.getLogger(FrmPrincipal.class.getName()).log(Level.SEVERE, null, ex);
        java.util.logging.Logger.getLogger(EditorFiles.class.getName()).log(java.util.logging.Level.SEVERE
        , null, ex);

        }
    }


}
```

# Dar funcionalidad al botón eliminar al dar click.

Aqui simplemente con el método delete se borra el archivo importado. Se usa el if para que si no se pudo borrar (ya sea problamento porque no se importó nada) muestre un mensaje.

```
private void btnEliminarMouseClicked(java.awt.event.MouseEvent evt) {                                         
    System.out.println("Inico eliminar archivo");
    File archivo = new File(this.txtArchivo.getText());
    if (archivo.delete()) {
        System.out.println("Archivo borrado: " + archivo.getName());
        txtArchivo.setText("");
    } else {
        System.out.println("Error al borrar el archivo");
    }
}                                        

```

# Funcionalidad del programa. 

1. Al dar clic en el botón Archivo, se busca un archivo json y se da a open:

![image](https://github.com/GerardoHP93/TareaFilesIO/assets/129221361/1c83f92f-6e20-4f44-b1ba-c715f7db0c8e)

![image](https://github.com/GerardoHP93/TareaFilesIO/assets/129221361/1a5f4d18-4096-485d-bc4d-6c841d823229)

![image](https://github.com/GerardoHP93/TareaFilesIO/assets/129221361/9a2b151f-1459-42b1-a773-f110246991bd)


2. Se modifican texto en el txtArea y se guarda.

![image](https://github.com/GerardoHP93/TareaFilesIO/assets/129221361/40f7cbd9-ae2d-4119-b3e4-31e42a2e1753)

![image](https://github.com/GerardoHP93/TareaFilesIO/assets/129221361/48e788a7-cad8-43f8-a6df-2e62d8988eed)

3. Se elimina el archivo.

![image](https://github.com/GerardoHP93/TareaFilesIO/assets/129221361/f48f5bc1-002c-4b07-91f0-a87e0b4e1d55)

![image](https://github.com/GerardoHP93/TareaFilesIO/assets/129221361/2def0797-1a52-4d97-9e27-9fecd2324695)


