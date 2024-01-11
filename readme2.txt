PlayerUI.cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using TMPro;
public class PlayerUI : MonoBehaviour
{
public Player player;
public TextMeshProUGUI coinsCounterText;
public Slider healthSlider;
void Update()
{

coinsCounterText.text = player.coins.ToString();

healthSlider.maxValue = player.maxHealth;
healthSlider.value = player.health;

}
}
Player.cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;
public class Player : MonoBehaviour
{
 
 public int health = 10;
 
 public int maxHealth = 10;
 
 public int coins;
 
 public GameObject fireballPrefab;
 public Transform attackPoint;
 
 public AudioSource audioSource;

 public AudioClip damageSound;

 public void TakeDamage(int damage)
 {
 health -= damage;

 if(health > 0)
 {
 audioSource.PlayOneShot(damageSound);

 }
 
 else
 {
 int sceneIndex = SceneManager.GetActiveScene().buildIndex;
 SceneManager.LoadScene(sceneIndex);
 }
 }

 public void CollectCoins()
 {
 coins++;

 }

 void Update()
 {

 if (Input.GetMouseButtonDown(0))
 {
 Instantiate(fireballPrefab, attackPoint.position, attackPoint.rotation);
 }
 }
}
Timer.cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;
using TMPro;
public class Timer : MonoBehaviour
{
 public int minutes;
 public float seconds;
 public TextMeshProUGUI timerText;

 void Update()
 {
 seconds -= Time.deltaTime;
 if (seconds <= 0)
 {
 if (minutes > 0)
 {
 seconds += 59;
 minutes--;
 }
 else
 {

 int sceneIndex = SceneManager.GetActiveScene().buildIndex;
 SceneManager.LoadScene(sceneIndex);
 }
 }

 int roundSeconds = Mathf.RoundToInt(seconds);
 timerText.text = minutes + ":" + roundSeconds;
 }
}