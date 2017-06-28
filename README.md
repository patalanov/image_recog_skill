# image recognition skill

Recognize contents of images using caffe bvlc_googlenet, 1000 categories available

# Deep draw

Visualize Layers using [deep draw](http://auduno.com/post/125837418083/drawing-with-googlenet), upload content to imgur

Representation of a Triceratops

![Image generated](https://i.imgur.com/CdSrfc5.png)


# install

        install caffe http://caffe.berkeleyvision.org/installation.html
        download bvlc_googlenet with caffe script
        add caffe_path to config or .py
        add imgur api to config or .py


# image recognition in other skills

        from os.path import dirname
        import sys
        sys.path.append(dirname(dirname(__file__)))

        from image_recog_skill import ImageRecognitionService

        def handle_img_recog_intent(self, message):
            classifier = ImageRecognitionService(self.emitter)
            path_to_file = "path/to/ur/image_file"
            results = classifier.local_image_classification(path_to_file)
            # make names pretty
            i = 0
            for result in list(results):
                # cleave first word nxxxxx
                result = result.split(" ")[1:]
                r = ""
                for word in result:
                    r += word + " "
                # split in "," since its same thing usually
                result = r[:-1].split(",")[0]
                results[i] = result
                i += 1
            self.speak("in test image i see " + results[0] + ", or maybe it is " + results[1])


# deep draw

        from os.path import dirname
        import sys
        sys.path.append(dirname(dirname(__file__)))

        from image_recog_skill import ImageRecognitionService

        def handle_img_recog_intent(self, message):
            imagenet_class = random.randint(0, len(self.label_mapping))
            classifier = ImageRecognitionService(self.emitter)
            classifier.local_deepdraw(imagenet_class, message.data.get("target"))


# image recog logs

        2017-06-17 15:31:16,508 - Skills - DEBUG - {"type": "recognizer_loop:utterance", "data": {"source": "cli:48736", "user": "48736", "utterances": ["cc"], "mute": true}, "context": null}
        2017-06-17 15:31:16,522 - Skills - DEBUG - {"type": "ImageRecognitionSkill:ImageClassfyStatusIntent", "data": {"confidence": 1.0, "target": "cli:48736", "mute": true, "intent_type": "ImageRecognitionSkill:ImageClassfyStatusIntent", "user": "48736", "utterance": "cc", "imgstatus": "cc"}, "context": {"target": "cli:48736"}}
        2017-06-17 15:31:16,530 - Skills - DEBUG - {"type": "speak", "data": {"target": "cli:48736", "mute": true, "expect_response": false, "more": false, "utterance": "Image Recognition is enabled", "metadata": {"source_skill": "ImageRecognitionSkill"}}, "context": null}
        2017-06-17 15:31:16,563 - Skills - DEBUG - {"type": "image_classification_request", "data": {"source": "cli:48736", "file": "/home/test/mycroft-server/server_skills/image_recog_service/obama.jpg"}, "context": null}
        2017-06-17 15:31:16,564 - ImageRecognitionSkill - INFO - loading image: /home/test/mycroft-server/server_skills/image_recog_service/obama.jpg
        2017-06-17 15:31:16,569 - ImageRecognitionSkill - INFO - predicting
        2017-06-17 15:31:30,240 - ImageRecognitionSkill - INFO - ['n04591157 Windsor tie', 'n04350905 suit, suit of clothes', 'n02865351 bolo tie, bolo, bola tie, bola', 'n02916936 bulletproof vest', 'n03838899 oboe, hautboy, hautbois']
        2017-06-17 15:31:30,246 - Skills - DEBUG - {"type": "speak", "data": {"target": "cli:48736", "mute": true, "expect_response": false, "more": false, "utterance": "in test image i see n04591157 Windsor tie, or maybe it is n04350905 suit, suit of clothes", "metadata": {"source_skill": "ImageRecognitionSkill"}}, "context": null}
        2017-06-17 15:31:30,252 - Skills - DEBUG - {"type": "message_request", "data": {"user_id": "cli:48736", "data": {"classfication": ["n04591157 Windsor tie", "n04350905 suit, suit of clothes", "n02865351 bolo tie, bolo, bola tie, bola", "n02916936 bulletproof vest", "n03838899 oboe, hautboy, hautbois"]}, "type": "image_classification_result"}, "context": null}
        2017-06-17 15:31:30,255 - Skills - DEBUG - {"type": "image_classification_result", "data": {"classfication": ["n04591157 Windsor tie", "n04350905 suit, suit of clothes", "n02865351 bolo tie, bolo, bola tie, bola", "n02916936 bulletproof vest", "n03838899 oboe, hautboy, hautbois"]}, "context": null}

# usage

        image recognition status <- recognize test image

        deep draw <- visualize a random layer (may takeup to 1 hour)

        deep draw with "class" <- fuzzy match your name to best availabel class and visualize it

# TODO

requirements.sh
deep draw logs
request from server usage / api doc


