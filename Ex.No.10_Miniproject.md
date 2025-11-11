## Ex.No: 10 — Implementation of 2D Game in Unity

Date:
Register Number:

## AIM:

To develop a 2D side-scrolling “Rock Blaster” game in Unity where the player controls a spaceship that shoots lasers to destroy incoming rocks using C# scripting and basic AI logic for object movement.

## Algorithm:
```
Start the Unity project and create a new 2D scene.

Design the background using a static image or tilemap.

Create the player object with movement controls using a Rigidbody2D or transform translation.

Add a laser prefab and script it to move forward when fired.

Implement shooting mechanics using a custom PlayerShooting script (laser instantiation).

Create the rock prefab and use a spawnManager script to spawn rocks at random intervals.

Write collision detection scripts so that when the laser hits the rock, both are destroyed.

Add score and sound effects (optional).

Test the game by running it and adjusting spawn positions, laser direction, and collision triggers.

Build and run the project to verify smooth gameplay and correct collision behavior.
```
## Program:
```
PlayerShooting.cs
using UnityEngine;

public class PlayerShooting : MonoBehaviour
{
    public GameObject laserPrefab;
    public float shootCooldown = 0.25f;
    public float forwardOffset = 1.0f;
    public float downwardOffset = -0.25f;
    private float lastShotTime;

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space) && Time.time > lastShotTime + shootCooldown)
        {
            Shoot();
            lastShotTime = Time.time;
        }
    }

    void Shoot()
    {
        Vector3 spawnPos = transform.position + new Vector3(forwardOffset, downwardOffset, 0f);
        Instantiate(laserPrefab, spawnPos, Quaternion.identity);
    }
}
```
```
Laser.cs
using UnityEngine;

public class Laser : MonoBehaviour
{
    public float speed = 10f;

    void Update()
    {
        transform.Translate(Vector2.right * speed * Time.deltaTime);
    }

    private void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Rock"))
        {
            Destroy(other.gameObject);
            Destroy(gameObject);
        }
    }
}
```
```
spawnManager.cs
using UnityEngine;
using System.Collections;

public class spawnManager : MonoBehaviour
{
    public GameObject rock;

    void Start()
    {
        StartCoroutine(SpawnRocks());
    }

    IEnumerator SpawnRocks()
    {
        while (true)
        {
            yield return new WaitForSeconds(Random.Range(3f, 6f));
            Vector3 pos = new Vector3(Random.Range(12f, 15f), -3.4f, 0f);
            Instantiate(rock, pos, Quaternion.identity);
        }
    }
}
```
```
Rock.cs
using UnityEngine;

public class Rock : MonoBehaviour
{
    public float speed = 3f;

    void Update()
    {
        transform.Translate(Vector2.left * speed * Time.deltaTime);
    }

    private void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player") || other.CompareTag("Laser"))
        {
            Destroy(gameObject);
        }
    }
}
```
## Output:

The player can shoot lasers from their spaceship to destroy incoming rocks.
The rocks spawn randomly from the right side and move left across the screen.
When the laser hits a rock, both objects are destroyed.
<img width="1481" height="933" alt="image" src="https://github.com/user-attachments/assets/2226f375-4622-4b76-b1ac-9e9a373bb160" />

## Result:
Thus, the 2D “Rock Blaster” game was successfully developed using Unity and implemented with AI-based random spawning and collision detection logic for dynamic gameplay.


