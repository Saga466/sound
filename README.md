
import javax.sound.sampled.*;

public class AudioRecorder {

    public static void main(String[] args) {
        AudioFormat format = new AudioFormat(AudioFormat.Encoding.PCM_SIGNED, 44100, 16, 2, 4, 44100, false);

        TargetDataLine line;
        DataLine.Info info = new DataLine.Info(TargetDataLine.class, format);

        if (!AudioSystem.isLineSupported(info)) {
            System.out.println("Line not supported");
            System.exit(0);
        }

        try {
            line = (TargetDataLine) AudioSystem.getLine(info);
            line.open(format);
            line.start();

            System.out.println("Recording...");

            AudioInputStream ais = new AudioInputStream(line);

            // Change this to your desired output file name
            String outputFile = "output.wav";
            AudioSystem.write(ais, AudioFileFormat.Type.WAVE, new java.io.File(outputFile));

            System.out.println("Recording completed.");

        } catch (LineUnavailableException | java.io.IOException e) {
            e.printStackTrace();
        }
    }
}
