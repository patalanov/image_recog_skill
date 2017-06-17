# image recognition skill


# install

        install caffe http://caffe.berkeleyvision.org/installation.html
        download bvlc_googlenet with caffe script
        add caffe_path to config


# using in other skills

        from os.path import dirname
        import sys
        sys.path.append(dirname(__file__) +"/image_recog_skill")

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



# skills logs

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

        image recognition status

# TODO

requirements.sh

