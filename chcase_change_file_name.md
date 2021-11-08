# Modifier le nom d'une série de fichiers : outil chcase



L’outil `chcase` vous permet de modifier une série de nom de fichier grâce à l’utilisation d’une expression régulière : c’est à dire un pattern qui devra être remplacé. 

Exemple :

On a des fichiers du type : 

    S002149_col_0_input_2-70070_R1_001.fastq  
    S002150_caa39_input_2-70071_R1_001.fastq  
    S002151_col_0_H3_1-70072_R1_001.fastq 
    S002152_col_0_H3_2-70073_R1_001.fastq

Le motif `70070_R1_001` n’apporte pas grand chose à l’identification du fichier mais change à chaque fichuer.

Pour supprimer ces parties peu informatives :

```bash
$ chcase -tx 's/-70..._R1_001//' *.fastq
```

La commande se décompose comme suit :

1. `chcase` : nom de la commande

2. les options : ce qui se trouve après le `-` . Dans ce cas il y en 2 le `t ` qui permet de tester et le `x` pour exécuter.

​	le ` -t` permet de tester le résultat de la commande. Le nom original des fichiers suivi du nom modifié s’affiche mais rien n’est modifier. Pour la modification le t devra être retiré.

3. L’expression régulière sous la forme ‘s/(quelque chose)/(autre chose)/‘

​	Le `s` pour substitute, indique que l’on va remplacer le premier élément par le second. ainsi dans l’exemple le premier élément `-70..._R1_001` est remplacé par rien (il n’y a rien entre les //).

​	Le motif remplacé se compose des parties fixes du pattern, au début et à la fin . La partie changeante, les 3 derniers chiffres (ici seul le dernier change mais si vous avez une longue liste d’autres chiffres pourraient changer) est représentée par 3 points. Le point signifie «un caractère quelconque».

4. Les fichiers à traiter, sous la forme `*.extension`. Cela signifie que tous les fichiers qui contiennent l’extension définie seront affectés par la modification à condition qu’ils contiennent dans leur nom le motif à remplacer. DAns l’exemple on a `*.fastq` ainsi tous les fichier en `.fastq` seront modifiés.



On obtient alors :


    S002149_col_0_input_2-70070_R1_001.fastq  =>  S002149_col_0_input_2.fastq
    S002150_caa39_input_2-70071_R1_001.fastq  =>  S002150_caa39_input_2.fastq
    S002151_col_0_H3_1-70072_R1_001.fastq  =>  S002151_col_0_H3_1.fastq
    S002152_col_0_H3_2-70073_R1_001.fastq  =>  S002152_col_0_H3_2.fastq

N’hésitez pas à me demander de l’aide pour des pattern plus complexe.

