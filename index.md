# draj
## Videos of some Interesting Projects
<table>
	<tr>
		<td>
			<iframe src="https://www.linkedin.com/embed/feed/update/urn:li:ugcPost:6629538307233673216?compact=1" allowfullscreen="" title="Embedded post" width="504" height="284" frameborder="0"></iframe>
		</td>
		<td>
			Training a car to drive on Bangalore roads (Reinforcement Learning)
			<iframe width="530" height="315" src="https://www.youtube.com/embed/wRFr0LPeoyE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
		</td>
	</tr>
</table>

## Serverless deployments DEMO
### Mobilenet Deployment
<table>
     <tr>
        <td>
          <input type="file" id="imageUpload" onchange="loadFile(event)"/>
          <img id="output" width="300" />
        </td>
 	<td>
  	      <li>First time might take ~45 seconds!</li>
  	      <li id="mobilenet_custom">MobileNet V2 (Winged Drones, Flying Birds, Quadcopters)</li>
        	<li id="mobilenet_imagenet">MobileNet V2 (ImageNet 1000 Classes)</li>
	     </td>
	</tr>
</table>
  <script>
  var loadFile = function(event) {
	var image = document.getElementById('output');
  const files = event.target.files
	
  image.src = URL.createObjectURL(files[0]);
  document.getElementById("mobilenet_custom").innerHTML = "Fetching results....."

  const formData = new FormData ();
  formData.append ("data", files[0]);
  console.log (formData);
  try {
	  fetch("https://ie8mujag6h.execute-api.ap-south-1.amazonaws.com/dev/classify", {
	    method: "POST",
	    body: formData,
	  })
	  .then(response => response.json())
	  .then(json => {
	    console.log (json);
	    if (json.error) {
	      document.getElementById("mobilenet_custom").innerHTML = json.error;
	    } else {
	      document.getElementById("mobilenet_custom").innerHTML = json.predicted[1];
	    }   
	   });

	  document.getElementById("mobilenet_imagenet").innerHTML = "Fetching results....."
	  fetch("https://flte7grm73.execute-api.ap-south-1.amazonaws.com/dev/classify", {
	    method: "POST",
	    body: formData,
	  })
		.then(response => response.json())
		.then(json => {
		  console.log (json);
	      if (json.error) {
		document.getElementById("mobilenet_imagenet").innerHTML = json.error;
	      } else {
		document.getElementById("mobilenet_imagenet").innerHTML = json.predicted[1];
	      }   
	   });
    } finally {
           setTimeout(() => {  console.log("World!"); 
 	   fetch("https://ie8mujag6h.execute-api.ap-south-1.amazonaws.com/dev/classify", {
	    method: "POST",
	    body: formData,
	  })
	  .then(response => response.json())
	  .then(json => {
	    console.log (json);
	    if (json.error) {
	      document.getElementById("mobilenet_custom").innerHTML = json.error;
	    } else {
	      document.getElementById("mobilenet_custom").innerHTML = json.predicted[1];
	    }   
	   });

	  document.getElementById("mobilenet_imagenet").innerHTML = "Fetching results....."
	  fetch("https://flte7grm73.execute-api.ap-south-1.amazonaws.com/dev/classify", {
	    method: "POST",
	    body: formData,
	  })
		.then(response => response.json())
		.then(json => {
		  console.log (json);
	      if (json.error) {
		document.getElementById("mobilenet_imagenet").innerHTML = json.error;
	      } else {
		document.getElementById("mobilenet_imagenet").innerHTML = json.predicted[1];
	      }   
	   });}, 45000);
	}
};
</script>
### Face Alignment [<a href="https://github.com/divyanshuraj6815/eva/tree/master/serverless_face_align">Source</a>]
<table>
     <tr>
        <td>
          <input type="file" id="imageUpload1" onchange="loadFile1(event)"/>
          <img id="output1" width="400" />
        </td>
 	<td>
		<li id="aligned_face">Aligned Face</li>
	<img id="aligned_image" src="data:image/png;base64, "/>
	</td>
    </tr>
</table>
  <script>
  var loadFile1 = function(event) {
  var image = document.getElementById('output1');
  const files = event.target.files
	
  image.src = URL.createObjectURL(files[0]);
  document.getElementById("aligned_face").innerHTML = "Fetching results....."
  document.getElementById("aligned_image").src = "data:image/png;base64, "

  const formData = new FormData ();
  formData.append ("data", files[0]);
  console.log (formData);
	  fetch("https://95w2ata4ll.execute-api.ap-south-1.amazonaws.com/dev/classify", {
	    method: "POST",
	    body: formData,
	  })
	  .then(response => response.json())
	  .then(json => {
	    console.log (json);
	    if (json.error) {
	      document.getElementById("aligned_image").innerHTML = json.error;
	    } else {
          	var str = json.aligned_image;
          	var res = str.slice (2, -1);
          	console.log (res);
		document.getElementById("aligned_face").innerHTML = "Aligned Face";
	      document.getElementById("aligned_image").src += res;
	    }   
	   });

};
</script>
### Face Swap [<a href="https://github.com/divyanshuraj6815/eva/tree/master/serverless_face_swap">Source</a>]
<table>
     <tr>
        <form>
        <td>
          <input type="file" id="imageUpload3" onchange="loadFile3(event)"/>
          <img id="output3" width="200" />
        </td>
        <td>
          <input type="file" id="imageUpload4"  onchange="loadFile4(event)"/>
          <img id="output4" width="200" />
        </td>
        </form>
	<td>
		<li id="swaped_face">Swaped Face</li>
		<img id="swaped_image" src="data:image/png;base64, "/>
	</td>
    </tr>
</table>
  <script>
  var loadFile3 = function(event) {
  var image1 = document.getElementById('output3');

  const files = event.target.files;
  console.log (files);
  image1.content = files[0]
  image1.src = URL.createObjectURL(files[0]);
  }
 
 var loadFile4 = function(event) {
  var image2 = document.getElementById('output4');

  const files = event.target.files;
  console.log (files);
  var image1 = document.getElementById('output3');
  image2.src = URL.createObjectURL(files[0]);

  document.getElementById("swaped_face").innerHTML = "Fetching results....."
  document.getElementById("swaped_image").src = "data:image/png;base64, "

  const formData = new FormData ();
  formData.append ("data1", image1.content);
  formData.append ("data2", files[0]);
  console.log (formData);
	  fetch("https://3mwpbz5gtb.execute-api.ap-south-1.amazonaws.com/dev/classify", {
	    method: "POST",
	    body: formData,
	  })
	  .then(response => response.json())
	  .then(json => {
	    console.log (json);
	    if (json.error) {
	      document.getElementById("swap_image").innerHTML = json.error;
	    } else {
          	var str = json.swaped_image;
          	var res = str.slice (2, -1);
          	console.log (res);
		document.getElementById("swaped_face").innerHTML = "Swaped Face";
	      document.getElementById("swaped_image").src += res;
	    }   
	   });

};
</script>
## Blogs Published on Medium
<table>
	<tr>
		<td style="height:200px;width:345px">
			<a href="https://medium.com/analytics-vidhya/learn-to-code-in-tensorflow2-fe735ad46826" target="_blank">
				<img src="https://miro.medium.com/max/875/1*Dl6GLvDip8VaUZiTcIl0QA.jpeg"/>
			</a>
			Data Augmentation with TF2
		</td>
		<td style="height:200px;width:345px">
			<a href="https://medium.com/@divyanshuraj.6815/learn-to-code-in-tensorflow2-part2-b1c448abbf1e" target="_blank">
				<img src="https://miro.medium.com/max/875/1*FNtUkoKczsNoRFLrY4vRbQ.png"/>
			</a>
			ResNet18 Model with TF2
		</td>
		<td style="height:230px;width:345px">
			<a href="https://medium.com/@divyanshuraj.6815/learn-to-code-in-tensorflow2-part3-7664926b9e69" target="_blank">
				<img src="https://miro.medium.com/max/634/1*_b_TQIZbHlwXp9XpmAJfcQ.jpeg"/>
			</a>
			Training with TF2
		</td>
	</tr>
</table>
<table>
	<tr>
		<td style="height:200px;width:400px">
			<a href="https://medium.com/@divyanshuraj.6815/not-interested-in-gardening-must-read-for-you-then-982a3bee1025" target="_blank">
				<img src="https://miro.medium.com/max/875/1*tCQAUFjCY14gF5154t8Fow.jpeg"/>
			</a>
			Gardening
		</td>
		<td style="height:200px;width:325px">
			<a href="https://medium.com/@divyanshuraj.6815/stuck-at-nan-not-a-number-while-training-your-model-4b5a6613f87e" target="_blank">
				<img src="https://miro.medium.com/max/875/1*S-OWN1vNP9scaZYV2hXyow.png"/>
			</a>
			How to get rid of NaN
		</td>
		<td style="height:200px;width:325px">
			<a href="https://medium.com/analytics-vidhya/relu-activation-increase-accuracy-by-being-greedy-6b93c7c40882" target="_blank">
				<img src="https://miro.medium.com/max/875/1*jqaW5OEqSVF6xjftzRkNnw.jpeg"/>
			</a>
			Playing with ReLU
		</td>
	</tr>
</table>
## Paintings published on Pinterest
<table>
	<tr>
		<td>
			<iframe src="https://assets.pinterest.com/ext/embed.html?id=763782418047880331" height="560" width="345" frameborder="0" scrolling="no" ></iframe>
		</td>
		<td>
			<iframe src="https://assets.pinterest.com/ext/embed.html?id=763782418041109141" height="597" width="345" frameborder="0" scrolling="no" ></iframe>
		</td>
		<td>
			<iframe src="https://assets.pinterest.com/ext/embed.html?id=763782418041109181" height="675" width="345" frameborder="0" scrolling="no" ></iframe>
		</td>
	</tr>
	<tr>
		<td>
			<iframe src="https://assets.pinterest.com/ext/embed.html?id=763782418041109125" height="520" width="345" frameborder="0" scrolling="no" ></iframe>
		</td>
		<td>
			<iframe src="https://assets.pinterest.com/ext/embed.html?id=763782418041109034" height="612" width="345" frameborder="0" scrolling="no" ></iframe>
		</td>
		<td>
			<iframe src="https://assets.pinterest.com/ext/embed.html?id=763782418041109044" height="560" width="345" frameborder="0" scrolling="no" ></iframe>
		</td>
	</tr>
	<tr>
		<td>
			<iframe src="https://assets.pinterest.com/ext/embed.html?id=763782418041109016" height="469" width="345" frameborder="0" scrolling="no" ></iframe>
		</td>
		<td>
			<iframe src="https://assets.pinterest.com/ext/embed.html?id=763782418041109191" height="574" width="345" frameborder="0" scrolling="no" ></iframe>
		</td>
		<td>
			<iframe src="https://assets.pinterest.com/ext/embed.html?id=763782418041108993" height="359" width="345" frameborder="0" scrolling="no" ></iframe>

		</td>
	</tr>
</table>
