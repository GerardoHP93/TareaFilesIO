# Proyecto: Aplicación que permita cargar un archivo de tipo .json, Editarlo y eliminarlo


# Alumno: Herrera Pacheco Gerardo Isidro ISC 4B 68612

## Se crea el JFrame con los elementos.

Se le añaden: 
TxtArea donde se mostrará el contenido del archivo seleccionado y tambien se podra editar el archivo ahi mismo
Boton Archivo. Para buscar y seleccionar el archivo
Botón guardar. Para guardar los cambios hechos en el archivo
Botón eliminar. Para eliminar el archivo
ComboBox. Para poder seleccionar el tipo de archivo a buscar (Esto yo se le lo agregue adicionalmente).
Y le di formato a los elementos.

IMAGEN

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


Tales métodos necesarios tales como: llenar los Estados (Estados que apareceran por defecto), para recorrer los Estados, eliminar,
añadir y actualizar, todo estos métodos seran llamados luego al hacer click en los botones de la interfaz.

