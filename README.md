# CSCI223_PromlemSet1_Couchenour

import java.text.DecimalFormat;
import java.util.Random;

public class Die {
	static int sides;

	public Die(int s) {
		sides = s;
	}

	static double[] pretendRoll(Die d) {
		double[] dist = new double[2 * sides + 1];
		for (int i = 1; i <= sides; i++)
			for (int j = 1; j <= sides; j++)
				dist[i + j] += 1.0;

		for (int k = 2; k <= 2 * sides; k++)
			dist[k] /= sides * 2;

		return dist;
	}

	static double[] realRoll(Die d, int rolls) {
		int d1, d2, sum;
		double[] results = new double[2 * sides + 1];
		for (int i = 1; i <= rolls; i++) {
			d1 = (int) (Math.random() * 6) + 1;
			d2 = (int) (Math.random() * 6) + 1;
			sum = d1 + d2;
			results[sum] += 1;
		}
		for (int k = 2; k <= 2 * sides; k++)
			results[k] /= sides * 2;

		return results;
	}

	public static void main(String[] args) {
		Die d1 = new Die(6);
		double[] empirical = pretendRoll(d1);
		double[] actual = realRoll(d1, 36);
		DecimalFormat df = new DecimalFormat("#.000");
		for (int n = 0; n <= (2 * d1.sides); n++) {
			System.out.println(df.format(empirical[n]) + "     " + df.format(actual[n]));
		}
	}

}
