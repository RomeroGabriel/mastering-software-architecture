# Analyzing Architecture Risk

`Every architectural design carries inherent risks`, whether they involving to availability, scalability, or data integrity. `Analyzing these risks constitutes a crucial aspect of the architectural process`. `Continuous risk analysis empowers architects to identify weaknesses within the design and proactively take corrective measures to mitigate potential issues`.

## Risk Matrix

`An initial challenge in evaluating architecture risks lies in the subjective classification of risks as low, medium, or high`. This subjectiveness can lead to ambiguity regarding the true risk levels in different parts of the architecture. `Architects can utilize a risk matrix to inject objectivity into the process and categorize risks` associated with specific architectural components.

`The architecture risk matrix employs two dimensions to assess risk: the overall impact of risk and the likelihood of its occurrence`. Each dimension is assigned a rating of low (1), medium (2), or high (3). These ratings are multiplied within each matrix grid, yielding an objective numerical representation of the risk.

!!! example
    ![Matrix for determining architecture risk from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/doc/images/matrix-risk.png)
    > Matrix for determining architecture risk from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

!!! example "Database Risk"
    Consider a scenario where there are concerns about the availability of a central database in the application. Initially, assess the impact dimension by `evaluating the potential consequences if the database were to go down`. An architect may determine this as a high-risk scenario, assigning a rating of 3 (medium), 6 (high), or 9 (high). However, `factoring in the second dimension, which evaluates the likelihood of the risk occurring`, the architect may realize that the database is hosted on highly available servers in a clustered configuration, minimizing the chances of unavailability. Consequently, `the intersection between high impact and low likelihood results in an overall risk rating of 3 (medium risk)`.
