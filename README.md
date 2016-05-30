# Stanford/Coursera Learning Assignments

These are the programming assignments from [Stanford/Coursera Machine Learning](https://www.coursera.org/learn/machine-learning) course taught by Andrew Ng.

My solutions to the programming exercises are written in Octave.

## Submission error when using Octave 4.0.0

At submit time, I encountered the following feedback:
```text
!! Submission failed: unexpected error: urlread: HTTP response code said error

!! Please try again later.
```

### One workaround

It seems that the conversion from ASCII to the hexadecimal escape the jsonlib uses is not working properly anymore in Octave 4.0. You can get it fixed by replacing

`str=[str str0(pos0(i)+1:pos(i)-1) sprintf('0x%X',str0(pos(i)))];`

with

`str=[str str0(pos0(i)+1:pos(i)-1) sprintf('0x%X',toascii(str0(pos(i))))];`

and

`str=sprintf('x0x%X_%s',char(str(1)),str(2:end));`

with

`str=sprintf('x0x%X_%s',toascii(str(1)),str(2:end));`

in `loadjson.m` and `makeValidFieldName.m`

### Another workaround (easier and the one I choose)

Followed the steps in https://learner.coursera.help/hc/en-us/community/posts/204693179-linear-regression-submit-error or in the Coursera Machine Learning forum https://www.coursera.org/learn/machine-learning/discussions/all/threads/vgCyrQoMEeWv5yIAC00Eog which is to apply the [patch](https://drive.google.com/file/d/0B6lXyE7fgSlXZjlqQ3FIRExmTDA/view)
