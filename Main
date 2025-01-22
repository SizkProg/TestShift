
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.nio.file.StandardOpenOption;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {

        String Zapusk = String.join(" ", args);
        //String Zapusk = "java -jar util.jar -o /some/path -f -a -p sample- in1.txt in3.txt in2.txt";
        String[] Commands = Zapusk.split(" ");

        String IntegerStr = "";
        String FloatStr = "";
        String StringStr = "";

        ArrayList <String> arrayListFile = new ArrayList<String>();

        //Переменные для статистики

        ArrayList<Integer> arrayListInt = new ArrayList<Integer>();
        ArrayList<Float> arrayListFloat = new ArrayList<Float>();
        ArrayList<String> arrayListString = new ArrayList<String>();

        String nameDirectory = System.getProperty("user.dir");
        String nameIntegers = "integers.txt";
        String nameFloat = "floats.txt";
        String nameStrings = "strings.txt";

        //Доп опции
        //-o  путь для результатов
        String path = "";
        //-p задает префикс
        String prefix = "";
        //-s краткая статистика
        boolean s = false;
        //-f полная статистика
        boolean f = false;
        //-a добавлять в существующие
        boolean a = false;

        for (int i = 0; i < Commands.length; i++) {
            if (Commands[i].equals("-o")) {
                path = Commands[i + 1] + "/";
            }
            if (Commands[i].equals("-p")) {
                prefix = Commands[i + 1];
            }
            if (Commands[i].equals("-s")) {
                s = true;
            }
            if (Commands[i].equals("-f")) {
                f = true;
            }
            if (Commands[i].equals("-a")) {
                a = true;
            }
            if (Commands[i].indexOf(".txt") != -1) {
                arrayListFile.add(Commands[i]);
            }
        }

        if (s == true && f == true) {
            System.out.println("Нельзя одновременно применять краткую и полную статистику");
            return;
        }

        try {
            Files.createDirectories(Paths.get(nameDirectory + path));
        } catch (IOException e) {

            System.err.println("Failed to create directory!" + e.getMessage());

        }

        Path INT = Path.of(nameDirectory + path + prefix + nameIntegers);
        Path FLOAT = Path.of(nameDirectory + path + prefix + nameFloat);
        Path STRING = Path.of(nameDirectory + path + prefix + nameStrings);

        for (String filesName : arrayListFile) {
try {
    List<String> list = Files.readAllLines(Path.of(nameDirectory + "/" + filesName));

    for (String str : list) {
        try {
            Integer z = Integer.parseInt(str);
            IntegerStr += str + "\n";
            arrayListInt.add(z);
        } catch (NumberFormatException nfe) {
            try {
                float b = Float.parseFloat(str);
                FloatStr += str + "\n";
                arrayListFloat.add(b);
            } catch (NumberFormatException nfe1) {
                StringStr += str + "\n";
                arrayListString.add(str);
            }
        }
    }
}
catch (IOException e){
    System.out.println("Не удалось найти файл с именем " + filesName);
}
        }

        if (!a) {
            if (Files.exists(INT)) {
                Files.deleteIfExists(INT);
            }
            if (Files.exists(FLOAT)) {
                Files.deleteIfExists(FLOAT);
            }
            if (Files.exists(STRING)) {
                Files.deleteIfExists(STRING);
            }


            if(IntegerStr.length()>0) {
                Files.createFile(INT);
                Files.writeString(INT, IntegerStr);
            }
            if(FloatStr.length()>0) {
                Files.createFile(FLOAT);
                Files.writeString(FLOAT, FloatStr);
            }
            if(StringStr.length()>0) {
                Files.createFile(STRING);
                Files.writeString(STRING, StringStr);
            }
        }
        else{
            try {
                Files.writeString(INT, IntegerStr, StandardOpenOption.APPEND);
            }
            catch (IOException e){
                System.out.println("Файл с типом Integer не создан, команда -a не отработала");
            }
            try {
                Files.writeString(FLOAT, FloatStr, StandardOpenOption.APPEND);
            }
            catch (IOException e){
                System.out.println("Файл с типом Float не создан, команда -a не отработала");
            }
            try {
                Files.writeString(STRING, StringStr, StandardOpenOption.APPEND);
            }
            catch (IOException e){
                System.out.println("Файл с типом String не создан, команда -a не отработала");
            }
        }



        if (s) {
            if(IntegerStr.length()>0) {
                System.out.println("Количество элементов типа Integer: " + arrayListInt.size());
            }
            if(FloatStr.length()>0) {
                System.out.println("Количество элементов типа Float: " + arrayListFloat.size());
            }
            if(StringStr.length()>0) {
                System.out.println("Количество элементов типа String: " + arrayListString.size());
            }
        }
        if (f) {
            if(IntegerStr.length()>0) {
                //int
                System.out.println("Количество элементов типа Integer: " + arrayListInt.size());
                System.out.println("Максимальный элемент типа Integer: " + Collections.max(arrayListInt));
                System.out.println("Минимальный элемент типа Integer: " + Collections.min(arrayListInt));
                System.out.println("Сумма элементов типа Integer: " + sumInt(arrayListInt));
                System.out.println("Среднее значение элементов типа Integer: " + averageInt(arrayListInt));
            }
            if(FloatStr.length()>0) {
                //float
                System.out.println("Количество элементов типа Float: " + arrayListFloat.size());
                System.out.println("Максимальный элемент типа Float: " + Collections.max(arrayListFloat));
                System.out.println("Минимальный элемент типа Float: " + Collections.min(arrayListFloat));
                System.out.println("Сумма элементов типа Float: " + sumFloat(arrayListFloat));
                System.out.println("Среднее значение элементов типа Float: " + averageFloat(arrayListFloat));
            }
            if(StringStr.length()>0) {
                //String
                System.out.println("Количество элементов типа String: " + arrayListString.size());
                System.out.println("Количество символов самой длинной строки: " + maxString(arrayListString));
                System.out.println("Количество символов самой короткой строки: " + minString(arrayListString));
            }
        }

    }

    static double averageInt(ArrayList<Integer> list) {

        double sum = 0;

        for (int i = 0; i < list.size(); i++) {
            sum += list.get(i);
        }

        return sum / list.size();
    }

    static float averageFloat(ArrayList<Float> list) {

        float sum = 0;

        for (int i = 0; i < list.size(); i++) {
            sum += list.get(i);
        }

        return sum / list.size();
    }

    static double sumInt(ArrayList<Integer> list) {

        double sum = 0;

        for (int i = 0; i < list.size(); i++) {
            sum += list.get(i);
        }

        return sum;
    }

    static float sumFloat(ArrayList<Float> list) {

        float sum = 0;

        for (int i = 0; i < list.size(); i++) {
            sum += list.get(i);
        }

        return sum;
    }

    static double minString(ArrayList<String> list) {

        int min = list.get(0).length();
        for (int i = 1; i < list.size(); i++) {

            min = (min > list.get(i).length() ? list.get(i).length() : min);

        }

        return min;
    }

    static double maxString(ArrayList<String> list) {

        int max = list.get(0).length();
        for (int i = 1; i < list.size(); i++) {

            max = (max < list.get(i).length() ? list.get(i).length() : max);

        }

        return max;
    }
}
