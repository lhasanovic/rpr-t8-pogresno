package ba.unsa.rpr.tutorijal8;

import java.io.File;
import java.net.URL;
import java.util.ResourceBundle;
import javafx.application.Platform;
import javafx.collections.FXCollections;
import javafx.collections.ObservableList;
import javafx.event.ActionEvent;
import javafx.fxml.FXML;
import javafx.fxml.Initializable;
import javafx.scene.control.Label;
import javafx.scene.control.ListView;
import javafx.scene.control.TextField;


public class FXMLDocumentController implements Initializable {

    @FXML
    private Label labela;
    @FXML
    private TextField uzorak;
    @FXML
    private ListView<String> lista;
    private ObservableList<String> fajlovi;

    @FXML
    private void handleDugmeTrazi(ActionEvent event) {
        fajlovi = FXCollections.observableArrayList();
        File folder = new File(System.getProperty("user.home"));
        File[] listaFajlova = folder.listFiles();

        Thread thread = new Thread (() -> {
            rekurzivnaPretraga(listaFajlova, folder);
        });
        thread.start();

        lista.setItems(fajlovi);
    }


    @Override
    public void initialize(URL url, ResourceBundle rb) {
        labela.setText("Uzorak:");
    }

    public void rekurzivnaPretraga(File[] listaFajlova, File folder) {
        if (listaFajlova != null) {
            for (File fajl : listaFajlova) {
                if (fajl.isFile() && fajl.getName().toLowerCase().contains(uzorak.getText().toLowerCase())) {
                    Platform.runLater(() -> {
                        fajlovi.add(folder.getPath() + File.separator + fajl.getName());
                    });
                } else if (fajl.isDirectory()) {
                    rekurzivnaPretraga(fajl.listFiles(), fajl);
                }
            }
        }
    }
}
