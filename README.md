# ST_Duke
[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/spatial-temporal-person-re-identification/person-re-identification-on-dukemtmc-reid)](https://paperswithcode.com/sota)

we achieve Rank@1=94.52%, mAP=84.09% without re-ranking and Rank@1=93.08%, mAP=91.95% with re-ranking

I prepared 4 models in this project. And you can change it with choosing models. You should note that there are two files that need to be modified.

  test_st_duke.py:  from line 19 to 22, change the model you want to inport.
  
  train_duke.py:    from line 24 to 27, change the model you want to inport.

### DukeMTMC-reID

    data prepare
    python3 prepare.py --Duke

    train (appearance feature learning)
    python3 train_duke.py --PCB --gpu_ids 2 --name ft_ResNet50_pcb_duke_e --erasing_p 0.5 --train_all --data_dir "/home/huangpg/st-reid/dataset/DukeMTMC_prepare/"

    test (appearance feature extraction)
    python3 test_st_duke.py --PCB --gpu_ids 2 --name ft_ResNet50_pcb_duke_e --test_dir "/home/huangpg/st-reid/dataset/DukeMTMC_prepare/"

    generate st model (spatial-temporal distribution)
    python3 gen_st_model_duke.py --name ft_ResNet50_pcb_duke_e --data_dir "/home/huangpg/st-reid/dataset/DukeMTMC_prepare/"

    evaluate (joint metric, you can use your own visual feature or spatial-temporal streams)
    python3 evaluate_st.py --name ft_ResNet50_pcb_duke_e

    re-rank
    6.1) python3 gen_rerank_all_scores_mat.py --name ft_ResNet50_pcb_duke_e
    6.2) python3 evaluate_rerank_duke.py --name ft_ResNet50_pcb_duke_e
