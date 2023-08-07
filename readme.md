# 实现4个LED灯同步亮灭

### Cubemx生成代码部分

使用Cubemx生成代码,你需要这样设置freeRTOS就行

![image-20230807150243957](Image/image-20230807150243957.png)

然后注意添加任务的优先级

![image-20230807150447658](Image/image-20230807150447658.png)

添加三个任务后再定义用于驱动LED的GPIO口

![image-20230807150534905](Image/image-20230807150534905.png)

然后生成代码就行

### Clion编辑代码部分

在生成的freertos.c文件中的第142行开始就是生成的任务函数写下LED灯闪烁的代码即可

```c
void Task_main_Start(void const * argument)
{
  /* USER CODE BEGIN Task_main_Start */
  /* Infinite loop */
  for(;;)
  {
      HAL_GPIO_TogglePin(LD2_GPIO_Port,LD2_Pin);
      osDelay(500);
  }
  /* USER CODE END Task_main_Start */
}

/* USER CODE BEGIN Header_StartTaskLED */
/**
* @brief Function implementing the myTaskLED thread.
* @param argument: Not used
* @retval None
*/
/* USER CODE END Header_StartTaskLED */
void StartTaskLED(void const * argument)
{
  /* USER CODE BEGIN StartTaskLED */
  /* Infinite loop */
  for(;;)
  {
      HAL_GPIO_TogglePin(LED1_GPIO_Port,LED1_Pin);
    osDelay(500);
  }
  /* USER CODE END StartTaskLED */
}

/* USER CODE BEGIN Header_StartTask03 */
/**
* @brief Function implementing the myTask03 thread.
* @param argument: Not used
* @retval None
*/
/* USER CODE END Header_StartTask03 */
void StartTask03(void const * argument)
{
  /* USER CODE BEGIN StartTask03 */
  /* Infinite loop */
  for(;;)
  {
      HAL_GPIO_TogglePin(LED2_GPIO_Port,LED2_Pin);
    osDelay(500);
  }
  /* USER CODE END StartTask03 */
}

/* USER CODE BEGIN Header_StartTask04 */
/**
* @brief Function implementing the myTask04 thread.
* @param argument: Not used
* @retval None
*/
/* USER CODE END Header_StartTask04 */
void StartTask04(void const * argument)
{
  /* USER CODE BEGIN StartTask04 */
  /* Infinite loop */
  for(;;)
  {
      HAL_GPIO_TogglePin(LED3_GPIO_Port,LED3_Pin);
    osDelay(500);
  }
  /* USER CODE END StartTask04 */
}
```

其他什么都不用,下载到开发板,看效果

![1691392245580](Image/1691392245580.jpg)

![1691392268282](Image/1691392268282.jpg)

结果是LED确实以500毫秒的事件闪烁起来
