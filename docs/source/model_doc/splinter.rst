.. 
    Copyright 2020 The HuggingFace Team. All rights reserved.

    Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with
    the License. You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on
    an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the
    specific language governing permissions and limitations under the License.

Splinter
-----------------------------------------------------------------------------------------------------------------------

Overview
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Splinter model was proposed in `Few-Shot Question Answering by Pretraining Span Selection
<https://arxiv.org/abs/2101.00438>`__ by Ori Ram, Yuval Kirstain, Jonathan Berant, Amir Globerson, Omer Levy. Splinter
is an encoder-only transformer (similar to BERT) pretrained using the recurring span selection task on a large corpus
comprising Wikipedia and the Toronto Book Corpus.

The abstract from the paper is the following:

In several question answering benchmarks, pretrained models have reached human parity through fine-tuning on an order
of 100,000 annotated questions and answers. We explore the more realistic few-shot setting, where only a few hundred
training examples are available, and observe that standard models perform poorly, highlighting the discrepancy between
current pretraining objectives and question answering. We propose a new pretraining scheme tailored for question
answering: recurring span selection. Given a passage with multiple sets of recurring spans, we mask in each set all
recurring spans but one, and ask the model to select the correct span in the passage for each masked span. Masked spans
are replaced with a special token, viewed as a question representation, that is later used during fine-tuning to select
the answer span. The resulting model obtains surprisingly good results on multiple benchmarks (e.g., 72.7 F1 on SQuAD
with only 128 training examples), while maintaining competitive performance in the high-resource setting.

Tips:

- Splinter was trained to predict answers spans conditioned on a special [QUESTION] token. These tokens contextualize
  to question representations which are used to predict the answers. This layer is called QASS, and is the default
  behaviour in the SplinterForQuestionAnswering class. Therefore:
- Use SplinterTokenizer (rather than BertTokenizer), as it already contains this special token. Also, its default
  behavior is to use this token when two sequences are given (for example, in the run_qa.py script).
- If you plan on using Splinter outside run_qa.py, please keep in mind the question token - it might be important for
  the success of your model, especially in a few-shot setting.
- Please note the 'initialize_new_qass' flag in SplinterConfig. It controls whether the QASS layer's pretrained
  parameters are used, or replaced with randomly initialized ones (see ablations in the paper for a detailed
  discussion).

This model was contributed by `yuvalkirstain <https://huggingface.co/yuvalkirstain>`__ and `oriram
<https://huggingface.co/oriram>`__. The original code can be found `here <https://github.com/oriram/splinter>`__.

SplinterConfig
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. autoclass:: transformers.SplinterConfig
    :members:


SplinterTokenizer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. autoclass:: transformers.SplinterTokenizer
    :members: build_inputs_with_special_tokens, get_special_tokens_mask,
        create_token_type_ids_from_sequences, save_vocabulary


SplinterTokenizerFast
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. autoclass:: transformers.SplinterTokenizerFast
    :members:


SplinterModel
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. autoclass:: transformers.SplinterModel
    :members: forward


SplinterForCausalLM
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. autoclass:: transformers.SplinterForCausalLM
    :members: forward


SplinterForMaskedLM
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. autoclass:: transformers.SplinterForMaskedLM
    :members: forward


SplinterForSequenceClassification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. autoclass:: transformers.SplinterForSequenceClassification
    :members: forward


SplinterForMultipleChoice
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. autoclass:: transformers.SplinterForMultipleChoice
    :members: forward


SplinterForTokenClassification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. autoclass:: transformers.SplinterForTokenClassification
    :members: forward


SplinterForQuestionAnswering
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. autoclass:: transformers.SplinterForQuestionAnswering
    :members: forward
