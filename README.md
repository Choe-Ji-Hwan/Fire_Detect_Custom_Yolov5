# Fire detect using custom datas and yolov5 From Colab
<div align="center">
  
<a href="https://colab.research.google.com/github/ultralytics/yolov5/blob/master/tutorial.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"></a>
<a href="https://www.kaggle.com/ultralytics/yolov5"><img src="https://kaggle.com/static/images/open-in-kaggle.svg" alt="Open In Kaggle"></a><br>
[**Python>=3.7.0**](https://www.python.org/) environment, including
[**PyTorch>=1.7**](https://pytorch.org/get-started/locally/).
  
</div>

- Process</br>
```
  1. Use yolov5 for tutorial
  2. Data custom (use roboflow or labelimg)
  3. trainning
    # 2-3 repeat
  4. comparison (yolov5 models, epoch, fire size)
```
## Used tool
<div align="center">
<table>
  <tr>
    <td>
      <img src="https://user-images.githubusercontent.com/54761791/161771200-8dabcba3-c09f-4311-a75c-55179a05cde0.png" />
    </td>
    <td>
      <img src="https://user-images.githubusercontent.com/54761791/161767737-e51233b9-232b-42e2-b0fc-6c02340f29c2.jpg" width="150" height="150"/>
    </td>
    <td>
      <img src="https://user-images.githubusercontent.com/54761791/161767484-6b17a39d-b6bf-416a-9b79-b14f49c00187.png" width="150" height="150"/>
    </td>
  </tr>
  <tr>
    <td align="center">
      <a href="https://github.com/ultralytics/yolov5">YOLOv5</a>
    </td>
    <td align="center">
      <a href="https://roboflow.com/">Roboflow</a>
    </td>
    <td align="center">
      <a href="https://colab.research.google.com/?utm_source=scs-index">Colab</a>
    </td>
  </tr>
</table>
</div>


## Result
<div align="center">

![Hnet com-image](https://user-images.githubusercontent.com/54761791/161439236-73a6c044-75f6-462e-8dde-cdaef96fc75c.gif)
![Hnet com-image](https://user-images.githubusercontent.com/54761791/161438769-097e2fea-6f0a-4494-b4dc-e8cba4541bba.gif)
  
</div>

<div></div>

## Sudo code
```
// detect tracing fire size 
fire_history := list()

while camera_on
	fire images info := {Yolov5 code}   // find fire and save box(tensor) info list

	while every fire boxes:
		center_point := ((box x1 + box x2) / 2, (box y1 + box y2) / 2)
		area := (box x1 - box x2) * (box y1 - box y2)
		
		// 10초 이상 업데이트 되지 않는 기록은 삭제
		for idx = len(fire_history) to 0 do
			if current_time - fire_history[idx][timer] > 10 then
					remove fire_history[idx]
		endfor

		// 같은 불의 center point update, diff update, 같은 불이면 area 누적, 시간 기록
		for f in all fire_history do
			if f[center][x] - f[diff][x] <= center_point[x] <= f[center][x] + f[diff][x]
				and f[center][y] - f[diff][y] <= center_point[y] <= f[center][y] + f[diff][y]
			  update f (center_point, diff, append area in array, time) in fire_history
				find = True
				break
		endfor
		if not find
			add new f (center_point, diff, area in array, time) in fire_history

		// sensitivity 이상의 크기 증가 횟수가 있다면 화재로 정의
		sensitivity := 2 (changeable)
		upper_cnt := 0

		for f in all fire_history do
			for idx = 1 to len(his[areas]) do
				change := fire_history[areas][idx-1] - fire_history[areas][idx]
				if change > 5
					print fire_history[center] 폭발 예상 발생

				if change > 0
					upper_cnt += 1
				else
					upper_cnt = 0
				if upper_cnt >= sensitivity
					print fire_history[center] 화재 발생
			endfor
		endfor
 
	endwhile
	{Yolov5 code} // print label box result to  

end while
```

## Used Dataset
Kaggle Fire Dataset: https://www.kaggle.com/phylake1337/fire-dataset </br>
cair/Fire-Detection-Image-Dataset images: https://github.com/cair/Fire-Detection-Image-Dataset</br>
Fire Image Data Set for Dunnings 2018 study-PNG still image set: https://collections.durham.ac.uk/files/r2d217qp536#.YkMMGShBxD_ </br>
