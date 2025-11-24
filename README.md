import org.apache.commons.math3.fitting.WeightedObservedPoints;
import org.apache.commons.math3.fitting.SimpleCurveFitter;
import org.apache.commons.math3.analysis.function.Identity; // For linear function

public class HousePricePrediction {

  public static void main(String[] args) {
        
   double[] squareFootage = {1400, 1600, 1700, 1875, 1100, 1550};
   double[] housePrices = {245, 280, 295, 340, 210, 260};

       
   WeightedObservedPoints obs = new WeightedObservedPoints();
        for (int i = 0; i < squareFootage.length; i++) {
            obs.add(squareFootage[i], housePrices[i]);
   }

       
   SimpleCurveFitter fitter = SimpleCurveFitter.create(new Identity(), null, new double[]{1, 1});

       
   double[] params = fitter.fit(obs.toList());

   double intercept = params[0];
   double slope = params[1];

  System.out.println("Linear Regression Equation: y = " + String.format("%.2f", slope) + "x + " + String.format("%.2f", intercept));

   double newSquareFootage = 1650;
   double predictedPrice = slope * newSquareFootage + intercept;
   System.out.println("Predicted price for " + newSquareFootage + " sq ft: $" + String.format("%.2f", predictedPrice) + "k");

   newSquareFootage = 2000;
   predictedPrice = slope * newSquareFootage + intercept;
   System.out.println("Predicted price for " + newSquareFootage + " sq ft: $" + String.format("%.2f", predictedPrice) + "k");
    }
}
