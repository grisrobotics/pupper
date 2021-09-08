import pigpio
from pupper.HardwareInterface import HardwareInterface
from pupper.Config import PWMParams, ServoParams
import numpy as np

def degrees_to_radians(input_array):
    """
    Converts degrees to radians.
    """
    return np.pi / 180.0 * input_array

def control_servos(hardware_interface):
    """
    Parameters
    ----------
    servo_params : ServoParams
        Servo parameters. This variable is updated in-place.
    pi_board : Pi
        RaspberryPi object.
    pwm_params : PWMParams
        PWMParams object.
    """
    # input k value
    k = float(
        input("Enter the scaling constant for your servo. This constant is how much you have to increase the pwm pulse width (in microseconds) to rotate the servo output 1 degree. (It is 11.333 for the newer CLS6336 and CLS6327 servos). Input: ")
    )
    hardware_interface.servo_params.micros_per_rad = k * 180 / np.pi
    hardware_interface.servo_params.neutral_angle_degrees = np.zeros((3, 4))

    while True:
        servos_degree = float(input("Enter the degree of the servos you want to reach(-90.0~90.0) or 100.0 to over:"))
        if servos_degree == 100.0:
            print("control over.")
            break
        print("control servos to degree: ", servos_degree)
    
        for leg_index in range(4):
            for axis in range(3):
                # Zero out the neutral angle
                hardware_interface.servo_params.neutral_angle_degrees[axis,leg_index] = 0
                # Move servo to set_point angle
                hardware_interface.set_actuator_position(
                    degrees_to_radians(servos_degree),
                    axis,
                    leg_index,
                )


def main():
    """Main program
    """
    hardware_interface = HardwareInterface()
    print("control begin.")
    control_servos(hardware_interface)
    print("\n\n control over!\n")


main()
