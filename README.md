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

```
    private void btnArchivoMouseClicked(java.awt.event.MouseEvent evt) {                                        
        System.out.println("Inico de la carga de archivo");
        JFileChooser fc = new JFileChooser();
        FileNameExtensionFilter filter = new FileNameExtensionFilter("Archivos de texto",cmboxTipoArchivo.getSelectedItem().toString());
        
        System.out.println(cmboxTipoArchivo.getSelectedItem().toString());
        
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

## Se crea algunos métodos modificar el ArrayList.

Tales métodos necesarios tales como: llenar los Estados (Estados que apareceran por defecto), para recorrer los Estados, eliminar,
añadir y actualizar, todo estos métodos seran llamados luego al hacer click en los botones de la interfaz.

