# Pseudo_Rigid_Body_Flexible_Beam
Pseudo-Rigid Body for Flexible Beam Analysis

### **Overall Summary**
The code models a structure consisting of 10 connected segments. Joints are placed between the segments with constraints that allow some degrees of freedom. A force-driven node is defined at the end, with forces applied and ramped up over time. The study runs an inverse dynamics simulation with force-dependent kinematics, aiming to analyze how forces act on the structure as it moves according to a predefined driver.

Overview of the code:

### 1. **Global Reference Frame**
   - A global reference frame (`GlobalRef`) is defined for the whole model.
   - A visual reference frame is created, with `Visible = On` and a small scale for display (`ScaleXYZ = {0.05, 0.05, 0.05}`).

### 2. **Segments Definition (`AnySeg`)**
   - The code defines 10 segments (S1 to S10). These segments likely represent sections of a mechanical structure like a beam or limb.
   - `r0` defines the position of the segment in 3D space.
   - `Mass` is set to 0, which means these segments are massless.
   - `Jii` (moments of inertia) are also set to zero, indicating no rotational inertia is considered for these segments.
   - Each segment has two reference nodes (`N1` and `N2`), representing the start and end points of the segment.
   - `AnyDrawPLine` is used to visually draw each segment, with a specified color (`RGB = {0.92, 0.77, 0.07}`).

### 3. **Joints Between Segments (`AnyStdJoint`)**
   - The segments are connected through standard joints (`AnyStdJoint`), with the first joint (`GRefS1`) connecting the global reference frame to the first segment.
   - For the joints between segments (e.g., `S1S2`, `S2S3`), constraints are defined. These constraints describe how the segments are connected, with some degrees of freedom fixed (Hard) and others dependent on forces (`ForceDep`).
   - `Reaction.Type` defines whether or not reaction forces are applied in different directions.

### 4. **Force and Springs**
   - A folder (`ForceAndSprings`) contains definitions for forces applied in the system.
   - `Stiffness` is defined as a constant value for the springs connecting the segments, with a negative value indicating a restoring force.
   - The `ConstraintForce` simulates the force between the last segment (`S10`) and a driven node (`DriveNode`). This force is applied with a gradual ramp-up using cosine functions.
   - There is also an alternative method (`ConstraintForce2`) provided for applying the constraint force, but it is commented out.

### 5. **Driver Definition (`Driver`)**
   - A driver (`driver_tip`) is defined to move the tip of the system (the last segment `S10`).
   - This driver specifies target positions (`DriverPos = {0.5, -0.3, 0, 0, 0, 0}`) for both linear and rotational components.

### 6. **Study Setup**
   - An `AnyBodyStudy` object is defined, which sets up the inverse dynamics simulation.
   - Gravity is set to zero (`Gravity = {0, 0, 0}`), meaning this is a gravity-free simulation.
   - The simulation runs from time `tStart = 0` to `tEnd = 1`, with `nStep = 200` steps.
   - The inverse dynamics study involves force-dependent kinematics (`ForceDepKinOnOff = On`), with specific perturbation and step sizes for the Newton method.

### 7. **Output (Commented)**
   - An `AnyOutputFile` is prepared but commented out. If uncommented, this section would save the positions of the segment reference nodes and some characteristics (like `stiffness`) to a file named `example.txt`.



Please cite this as:

```
@Article{biomechanics4030040,
AUTHOR = {Hahnemann, Yannis and Weiss, Manuel and Bernek, Markus and Boblan, Ivo and Götz, Sebastian},
TITLE = {Advancing Biomechanical Simulations: A Novel Pseudo-Rigid-Body Model for Flexible Beam Analysis},
JOURNAL = {Biomechanics},
VOLUME = {4},
YEAR = {2024},
NUMBER = {3},
PAGES = {566--584},
URL = {https://www.mdpi.com/2673-7078/4/3/40},
}
```
