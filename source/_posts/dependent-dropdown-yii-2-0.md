---
title: dependent dropdown yii 2.0
date: 2018-10-04 17:33:48
tags:
---

The View

<?php 
    $dataBuilding = ArrayHelper::map(DclBuilding::find()->asArray()->all(), 'id', 'name');
    echo $form->field($model, 'building_id')->dropDownList($dataBuilding,
        [
            'prompt'=>Yii::t('app', 'Pilih Gedung'),
            'onchange'=>'
            $.post( "'.Yii::$app->urlManager->createUrl('pemesanan/listfloor?id=').'"+$(this).val(), function( data ) {
            $( "select#floor" ).html( data );
            });'
        ]);
?>

        <?php 
            $dataFloor = ArrayHelper::map(DclFloor::find()->asArray()->all(), 'id', 'floor');
            echo $form->field($model, 'floor_id')->dropDownList($dataFloor,
                [
                    // 'prompt'=>'-Pilih Lantai-',
                    'id' => 'floor',
                    'onchange' => '
                    $.post( "'.Yii::$app->urlManager->createUrl('pemesanan/listroom?id=').'"+$(this).val(), function( data ) {
                    $( "select#room" ).html( data );
                    });'
                ]);
        ?>

The Controller

    public function actionListfloor($id)
    {
        $countFloors = DclFloor::find()->where(['building_id' => $id])->count();
        $floors = DclFloor::find()->where(['building_id' => $id])->orderBy('id ASC')->all();
        
        if($countFloors > 0){
            foreach($floors as $floor){
                echo "<option value='".$floor->id."'>".$floor->floor."</option>";
            }
        }
        else{
            echo "<option>-</option>";
        }
    }
