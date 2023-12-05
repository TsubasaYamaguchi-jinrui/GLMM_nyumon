# 本稿の目的    
## なぜGLMやGLMMについて学ぶ必要があるのか？    
近年、生態学や動物行動学をはじめ、複雑な生物学のデータを解析する手法が発達してきています。これは、従来のシンプルな統計手法(e.g. t検定、カイ二乗検定、線形回帰など)では、これらの分野で扱う複雑なデータを分析するには不適切であることが分かってきているからです(Harrison et al., 2018)。  

様々な分析のなかでも、**線形モデル(linear model)**や**線形混合モデル(linear mixed model)**、およびこれらを様々な分布のデータに拡張した**一般化線形モデル(generalized linear model)**や**一般化線形混合モデル(generalized linear mixed model)**などは2000年代以降急速に用いられるようになってきています(Bolker et al., 2009; Fox et al., 2015; Zuur, 2009; 大東, 2010)。図は、Google Scholarを用いて、動物行動学・生態学・霊長類学の分野で著名な学術雑誌において、"linear model"、"linear mixed model(LMM)"、"generalized linear model (GLM)"、"generalized linear mixed model (GLMM)"、という単語が出てきた論文の割合を示したものです(2023年8月18日時点)。私たちが普段読む/投稿することが多いこれらの雑誌においても、2000年代以降これらの分析手法が数多く使われるようになってきたことが示唆されます(特に行動学系では)。同様の分析に異なる名称が用いられていることもある(e.g., "ANOVA"、"ANCOVA"、"linear regression"など)ことを考慮すると、実際の割合はもっと高くなるはずです。

![GLMやGLMMなどの単語を含む論文の割合](image/journal.png)  

このことは、もはやこれらの分析についてきちんと理解しなければ、多くの論文の分析結果を適切に解釈できないということを示します。分析への理解が不十分であれば、仮に論文の著者が分析を誤用していたり、分析結果を誤って解釈していたりしても(実際にそのような論文はある)、論文の内容を鵜呑みして引用してしまうことになりかねません。これは大きな問題です。

またこうした流れの中で、私たち自身も論文を執筆する際に、これらの分析を使用することを求められることがますます増えていくのではないかと予想されます。そのとき、GLMやGLMMについてあまり理解しないままに分析を行えば、自身のデータに対して不適切な分析を行ってしまったり、分析結果を誤って解釈してしまったりするかもしれません。

以上のことから、本稿はGLM/GLMMが用いられた分析結果について適切に理解できるようになることに加え、可能であればRを用いて自身のデータについてもGLM/GLMMを用いた分析ができるようになることを目標に作成されました。私自身まだ理解が及ばないところもありますが、本稿を読んでお役に少しでも立てれば幸いです。

## 本稿で扱う内容  
本稿で扱うのは、以下の内容です。  

- 確率と統計の基本  
- 統計モデリングとは何か   
- 一般化線形モデル(GLM)   
- 一般化線形混合モデル(GLMM)   
- 結果の診断と統計検定   
- モデル選択   
- 発展的なモデル(ゼロ過剰モデル、ハードルモデル)  

参考にしたのは主に以下の文献です。特に日本語で示した文献は、GLMやGLMMの入門としてはうってつけだと思います。  
なお、本稿の作成に使用したファイルとRのコードは筆者のGithubですべて閲覧できます。   

- 馬場真哉(2015) 平均・分散から始める一般化線形モデル入門 (馬場, 2015)  
- 粕谷英一(2012) 一般化線形モデル (松浦, 2012)  
- Gelman et al. (2020) Regression and Other Stories (Gelman et al., 2020)  
- Fox et al. (2015) Ecological Statistics: Contemporary Theory and Application (Fox et al., 2015)  
- Dunn & Smyth (2018) Generalized Linear Models with Examples in R (Dunn & Smyth, 2018)  
- 馬場真哉(2019) RとStanではじめるベイズ統計モデリングによるデータ分析 (馬場, 2019)  
- 松浦健太郎(2016) StanとRでベイズ統計モデリング (松浦, 2016)   
- McElreath, R (2020) Statistical Rethinking (McElreath, 2009)  

本稿はRの基本操作とtidyverseパッケージによるデータハンドリングができることを前提としています。tidyverseパッケージを用いたデータ処理については、以下の書籍などを参照してください。

- R for Data Science (Wickham & Grolemund, 2016)
- R Graphics Coocbook 2nd Edition (Chang, 2018)  
- RユーザのためのRstudio[実践]入門~tidyverseによるモダンな分析フローの世界 改訂2版 (松村 et al., 2021)   

**References**  
Bolker, B. M., Brooks, M. E., Clark, C. J., Geange, S. W., Poulsen, J. R., Stevens, M. H. H., & White, J. S. S. (2009). Generalized linear mixed models: A practical guide for ecology and evolution. In Trends in Ecology and Evolution (No. 3; Vol. 24, pp. 127–135).  
Chang, W. (2018). R graphics cookbook: Practical recipes for visualizing data. “O’Reilly Media, Inc.”  
Dunn, P. K., & Smyth, G. K. (2018). Generalized linear models with examples in R. Springer New York.   
Fox, G. A., Negrete-Yankelevich, S., & Sosa, V. J. (2015). Ecological statistics: Contemporary theory and application. Oxford University Press.  
Gelman, A., Hill, J., & Vehtari, A. (2020). Regression and other stories. Cambridge University Press.   
Harrison, X. A., Donaldson, L., Correa-Cano, M. E., Evans, J., Fisher, D. N., Goodwin, C. E. D., Robinson, B. S., Hodgson, D. J., & Inger, R. (2018). A brief introduction to mixed effects modelling and multi-model inference in ecology. PeerJ, 2018(5).  
McElreath, R. (2009). Statistical rethinking: A bayeasian course with example in r and stan. CRC Press.  
Wickham, H., & Grolemund, G. (2016). R for data science: Import, tidy, transform, visualize, and model data. “O’Reilly Media, Inc.”  
Zuur, A. F. (2009). Mixed effects models and extensions in ecology with R. Springer.  
大東健太郎. (2010). 線形モデルから一般化線形モデル（GLM）へ. 雑草研究, 55(4), 268–274.  
松村優哉., 湯谷啓明., 紀ノ定保礼., & 前田和. (2021). RユーザのためのRstudio[実践]入門 tidyverseによるモダンな分析フローの世界 改訂2版. 技術評論社.  
松浦健太郎. (2012). StanとRでベイズ統計モデリング. 共立出版.  
松浦健太郎. (2016). StanとRでベイズ統計モデリング. 共立出版.  
馬場真哉. (2015). 平均・分散から始める一般化線形モデル入門. プレアデス出版.  
馬場真哉. (2019). RとStanではじめるベイズ統計モデリングによるデータ分析. 講談社.  
