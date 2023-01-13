```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    // Public float variable to set the speed of the player movement from the Unity Inspector
    public float speed = 10.0f;
    // Public float variable to set the jump force of the player from the Unity Inspector
    public float jumpForce = 10.0f;

    // Private Rigidbody variable to store the Rigidbody component of the player object
    private Rigidbody rb;

    void Start()
    {
        // Get the Rigidbody component of the player object and store it in the rb variable
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        // Get input from the horizontal axis (usually the left stick on a gamepad or the A,D keys on a keyboard)
        float moveHorizontal = Input.GetAxis("Horizontal");
        // Get input from the vertical axis (usually the left stick on a gamepad or the W,S keys on a keyboard)
        float moveVertical = Input.GetAxis("Vertical");

        // Create a new Vector3 variable with the input values, used to move the player
        Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);

        // Add force to the Rigidbody in the direction of the movement vector, multiplied by the speed
        rb.AddForce(movement * speed);

        // Check if the space key is pressed
        if (Input.GetKeyDown(KeyCode.Space))
        {
            // Add an upward force to the Rigidbody, simulating a jump
            rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
        }
    }
}
```