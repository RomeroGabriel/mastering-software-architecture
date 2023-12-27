# Analyzing Architecture Risk

`Every architectural design carries inherent risks`, whether they involving to availability, scalability, or data integrity. `Analyzing these risks constitutes a crucial aspect of the architectural process`. `Continuous risk analysis empowers architects to identify weaknesses within the design and proactively take corrective measures to mitigate potential issues`.

## Risk Matrix

`An initial challenge in evaluating architecture risks lies in the subjective classification of risks as low, medium, or high`. This subjectiveness can lead to ambiguity regarding the true risk levels in different parts of the architecture. `Architects can utilize a risk matrix to inject objectivity into the process and categorize risks` associated with specific architectural components.

`The architecture risk matrix employs two dimensions to assess risk: the overall impact of risk and the likelihood of its occurrence`. Each dimension is assigned a rating of low (1), medium (2), or high (3). These ratings are multiplied within each matrix grid, yielding an objective numerical representation of the risk.

!!! example
    ![Matrix for determining architecture risk from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/doc/images/risk/matrix-risk.png)
    > Matrix for determining architecture risk from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

!!! example "Database Risk"
    Consider a scenario where there are concerns about the availability of a central database in the application. Initially, assess the impact dimension by `evaluating the potential consequences if the database were to go down`. An architect may determine this as a high-risk scenario, assigning a rating of 3 (medium), 6 (high), or 9 (high). However, `factoring in the second dimension, which evaluates the likelihood of the risk occurring`, the architect may realize that the database is hosted on highly available servers in a clustered configuration, minimizing the chances of unavailability. Consequently, `the intersection between high impact and low likelihood results in an overall risk rating of 3 (medium risk)`.

## Risk Assessments

`A risk assessment serves as a concise overview of an architecture's overall risk`, contextualized against specific assessment criteria. Leveraging the [risk matrix](#risk-matrix) becomes pivotal in constructing meaningful risk assessments.

While the format of risk assessments can vary, `they generally encapsulate the risk, as qualified by the risk matrix, associated with particular assessment criteria within the application's services or domain areas`. The typical report format employs use (1-2) denoting `low risk`, (3-4) indicating `medium risk`, and (6-9) signifying `high risk`. Often color-coded as green (low), yellow (medium), and red (high), these shades facilitate interpretation for both color and non-color users. `Cumulative risk can be calculated for each criterion and service/domain area`.

!!! example
    ![Example of a standard risk assessment from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/doc/images/risk/assess-example.png)
    > Example of a standard risk assessment from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

    Notice the accumulated risk for data integrity is the highest at 17, while availability registers the least risk at 10. Relative risk for each domain area can also be determined with customer registration posing the highest risk and order fulfillment the lowest.

`These numbers offer a basis for tracking improvements or deteriorations within specific risk categories or domain areas`.

In practice, `not all risk analysis results are presented simultaneously`. Filtering becomes imperative to convey a targeted message in a given context. For instance, `in a meeting focusing on high-risk areas, filtering can spotlight only those areas, enhancing clarity and maintaining a favorable signal-to-noise ratio and presenting a clear picture of the state of the system (good or bad)`.

### Tracking Trends: Improvement or Deterioration

`The presented assessment report offers a snapshot in time, lacking insights into whether conditions are improving or getting worse`. To address this, incorporate directional indicators such as plus (+) and minus (-) signs next to the risk ratings.

!!! example
    ![Showing direction of risk with plus and minus signs from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/doc/images/risk/assess-example-sinal.png)
    > Showing direction of risk with plus and minus signs from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

    Examining the example, `while the performance for customer registration is medium (4), the minus sign signifies a worsening trend, approaching high risk`. Conversely, the high scalability rating for catalog checkout is accompanied by a plus sign, signaling improvement. `Ratings without directional signs indicate stable risk conditions, neither improving nor worsening`.

!!! example "An Alternative Approach"
    ![Showing direction of risk with arrows and numbers from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/doc/images/risk/assess-example-sinal-alt.png)
    > Showing direction of risk with arrows and numbers from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

Continuous measurements facilitated by [fitness functions](../arch_characteristics/measuring_governing.md#fitness-functions) `shows direction of risk, allowing for trend analysis and determining the directional trajectory of each risk factor`.
